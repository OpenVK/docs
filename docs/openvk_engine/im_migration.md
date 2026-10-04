# IM Migration & Setup Guide

In modern versions of OpenVK, instant messaging (dialogues, group chats, LongPoll real-time updates) has been decoupled into an external, high-performance Go microservice backed by Redis and its own database schema.

This guide details how to install the IM microservice, configure OpenVK, migrate legacy messages from an older database, and set up the LongPoll reverse proxy.

---

## Architecture Overview

```
[ Web Browser / Mobile Client ]
   │
   ├─► HTTP /im, /method/*  ────────► [ OpenVK PHP Core / VKAPI ]
   │                                         │
   │                                         ▼ (IMBroker / Redis Token)
   │                                  [ Go IM Microservice ]
   │                                         │
   └─► HTTP LongPoll (/nim) ◄────────────────┘ (Message storage / Event queue)
```

- **Go IM Microservice**: Handles message persistence, chat metadata, ACLs, read/unread states, and serves the real-time LongPoll server on `/nim`.
- **Redis**: Coordinates short-lived authentication tokens (`im:session:api:*`) and tracks real-time user online presence (`im:online_users`).
- **OpenVK Core (PHP)**: Communicates with the microservice via `openvk\Web\Util\IMBroker` and exposes standard VK API `messages.*` endpoints.

---

## Prerequisites

Ensure the following dependencies are installed and running on your server:

1. **Go** (version 1.18 or newer)
2. **Redis Server** (version 5.0+)
3. **MySQL / MariaDB** (version 5.7+ / MariaDB 10.3+)
4. **Nginx** (or compatible reverse proxy)

---

## Step 1: Clone and Build the IM Microservice

Clone the IM service repository into your preferred directory (for example, `/opt/im`):

```bash
git clone https://github.com/openvk/openvk-im.git /opt/openvk-im
cd /opt/openvk-im
```

Build the binary (or run directly with Go):

```bash
go build -o im .
```

---

## Step 2: Initialize / Update the Database Schema

Before starting the service or migrating old data (as well as after updating the service), run the schema migration command:

```bash
# Using go run:
go run . db create

# Or using the compiled binary:
./im db create
```

> [!NOTE]
> `db create` executes GORM auto-migrations. It automatically creates new tables, missing columns, and indexes without dropping or corrupting existing data. You should also run this command when updating the IM microservice to apply any new database schema changes.

---

## Step 3: Migrate Legacy Messages

If upgrading an existing OpenVK instance that previously used monolithic database message tables:

1. Make sure your main OpenVK database is accessible and configured in the IM service configuration.
2. Run the legacy migration command:

```bash
# Using go run:
go run . db migrate-legacy

# Or using the compiled binary:
./im db migrate-legacy
```

### What gets migrated:
- Direct private messages and historical dialogues.
- Group chats, titles, and participant lists.
- Attachments (photos, videos, audios, documents, stickers).
- Read/unread statuses, flags, and original timestamps.

---

## Step 4: Configure OpenVK (`openvk.yml`)

Open your `openvk.yml` configuration file (usually in `/opt/openvk/openvk.yml`):

```yaml
openvk:
    credentials:
        # Redis connection
        redis:
            addr: "127.0.0.1"
            port: 6379
            password: ""

        # Instant Messaging microservice connection
        im:
            enable: true
            server_url: "http://127.0.0.1:8080"  # Internal HTTP URL of the Go microservice
            lp_server_addr: "openvk.example.com" # Public domain/host for LongPoll clients
```

### Configuration parameters:
- `enable` — enables IM integration in OpenVK (`true` / `false`). When disabled, the `/im` route renders a maintenance page.
- `server_url` — internal endpoint where OpenVK PHP makes RPC/API calls to the microservice.
- `lp_server_addr` — external hostname returned in `messages.getLongPollServer` for browser and client connections.

---

## Step 5: Configure Nginx Reverse Proxy

Add the `/nim` location block to your OpenVK Nginx server block to route LongPoll requests to the microservice without buffering:

```nginx
server {
    server_name openvk.example.com;

    # ... existing OpenVK configuration ...

    # LongPoll endpoint for instant messages
    location /nim {
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header Connection "";
        
        # Critical for LongPoll streaming:
        proxy_buffering off;
        proxy_read_timeout 60s;
        proxy_send_timeout 60s;
    }
}
```

Reload Nginx after saving:

```bash
sudo nginx -t && sudo systemctl reload nginx
```

---

## Step 6: Set Up Systemd Service

To keep the IM microservice running in the background and start automatically on boot, create a systemd unit file:

```ini
# /etc/systemd/system/openvk-im.service
[Unit]
Description=OpenVK Instant Messaging Service
After=network.target redis.service mysql.service

[Service]
Type=simple
User=www-data
Group=www-data
WorkingDirectory=/opt/openvk-im
ExecStart=/opt/openvk-im/im
Restart=always
RestartSec=5
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
```

Enable and start the service:

```bash
sudo systemctl daemon-reload
sudo systemctl enable --now openvk-im
sudo systemctl status openvk-im
```

---

## Step 7: Verification & Troubleshooting

### 1. Health Check
Verify that the LongPoll server is responding correctly:

```bash
curl http://openvk.example.com/nim?health=1
```
The expected output is:
```
OK
```

### 2. Maintenance Screen on `/im`
If visiting `/im` displays a maintenance error:
- Ensure `openvk-im.service` is running (`systemctl status openvk-im`).
- Verify Redis is running and reachable (`redis-cli ping` returns `PONG`).
- Check `openvk.credentials.im.enable: true` in `openvk.yml`.

### 3. Real-Time Events Not Updating
If messages send successfully but incoming messages do not appear without refreshing:
- Check that `proxy_buffering off;` is set in the Nginx `/nim` block.
- Open the browser developer console and enable verbose logging:
  ```javascript
  localStorage.setItem('tw.im.verbose_logging', '1');
  ```
  Reload the page to inspect incoming LongPoll events in the console.
