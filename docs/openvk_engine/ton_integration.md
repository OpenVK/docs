# TON integration

If you have commerce turned on and you really want to sell "voices" for real money, there is a thing called "TON Integration".

To configure this, firstly you should turn it on in `openvk.yml` config file:

```yaml
ton:
    enabled: true
    address: "ZHOPAkAkaKsechHki61345618348eu9ihf"
    testnet: false
    rate: 0.02
    regex: "ovk=([0-9]+)"
    hint: "ovk=$1"
```

**Where:**

`address` is the your wallet address (you can make in on [TON Wallet](https://wallet.ton.org) website, mobile apps like Tonkeeper or Toncoin Wallet, available both on Android and iOS, or trough Telegram bots (not recommended))

`rate` - the currency of voices per TON

`regex` and `hint` - the way to identify a user by ID (it's better to leave it as default)

**Next**, add a task to a crontab:

```sh
crontab -e
```

And add this to the text editor that just opened up:

```cron
*/1 * * * * php /path/where/is/your/openvk/installation/is/located/openvkctl fetch-ton
```

This thing will check for new transactions every minute. 

**And you're actually done!** Enjoy your TONs!
