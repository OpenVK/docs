# About Chandler
[Chandler](https://github.com/openvk/chandler) is PHP-based web framework. By itself it's pretty useless, but you can install plugins/apps.

Chandler provides the foundation — routing, ORM, templating, auth, sessions, email, and captcha — while apps register themselves as builtin extensions and supply the actual pages.

## Features

- **Routing** — YAML-defined routes with typed placeholders (`{num}`, `{text}`, `{slug}`, custom `{?regex}`)
- **ORM** — Nette Database with ActiveRow-style `DBEntity` models, soft-delete, change logging
- **Templating** — [Latte](https://latte.nette.org) engine with custom `{css}`, `{script}`, `{presenter}` tags
- **Auth** — Argon2id password hashing, session tokens (JWT), IP/UA validation
- **Captcha** — built-in, served as WebP, stored captcha with encryption
- **Email** — Symfony Mailer SMTP or Postmark API
- **Events** — `EventDispatcher` for hook-based plugins
- **Console** — Symfony Console commands
- **Config** — YAML with disk caching
- **DI** — Nette DI container per app namespace

## State of Chandler
This product is still in development phase, we are currently writing documentation/tests and API is going to change.

## Installation guide
Check [this](https://github.com/OpenVK/chandler/blob/master/USAGE.md).
