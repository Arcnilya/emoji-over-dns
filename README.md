# Emoji over DNS

This is a lab using docker compose to experiment with DNS and emoji short-code mapping to domain names.

Emojis are structured in a hierarchy which maps very well onto DNS:
```
normal.smile.emoji. -> ":smile:" 😄
slight.smile.emoji. -> ":slight_smile:" 🙂
sweat.smile.emoji. -> ":sweat_smile:" 😅
cat.smile.emoji. -> ":smile_cat:" 😸
```

This repo consists of a "emoji" TLD name server and a "smile" SLD name server.
Their folders contains a zone file, a named.conf.local file and a Dockerfile.

## How to run
Make sure that you have docker/-compose
```sh
sudo docker compose up -d
```

## How to test
Query the TLD directly, which will refer to the SLD
```sh
dig @10.0.0.53 cat.smile.emoji TXT
```

Get all available smileys using zone transfer
```sh
dig @10.0.1.53 smile.emoji AXFR | grep TXT
```

## How to turn off
```sh
sudo docker compose down
```

