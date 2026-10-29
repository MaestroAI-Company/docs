---
title: PrivateBin instance
description: Change the PrivateBin server that hosts shared conversations, and why you would.
---

Shared conversations are uploaded as encrypted pastes to a PrivateBin instance. The default instance is `privatebin.net`. Opera lets you point at another instance, including one you host yourself, in **Settings → Privacy → Shared conversations server**.

## How sharing works

When you share a conversation:

1. Opera encrypts the conversation on your device with a random 256-bit key.
2. The encrypted paste is uploaded to the PrivateBin instance.
3. The decryption key stays in the URL fragment (the part after `#`), which browsers never send to the server.

The instance stores ciphertext it cannot read. It also enforces a retention policy: pastes expire after three days by default.

## Why change the URL

- **Data control**: the default instance is run by the PrivateBin project. Self-hosting keeps your pastes on hardware you control.
- **Trust**: for sensitive conversations, you may prefer a server you administer, or one inside your own network.
- **Availability**: if `privatebin.net` is down or slow, a mirror or your own instance keeps sharing working.
- **Compliance**: in some settings, sending encrypted data to a third-party server is not acceptable even if the server cannot read it.

:::note
Changing the instance only affects new shares. Links you already created keep pointing at the instance that hosts them, so old links keep working as long as that instance keeps the paste.
:::

## Change the instance

1. Open **Settings → Privacy → Shared conversations server**.
2. Enter the address of your PrivateBin instance, for example `https://paste.example.net`.
3. Leave the field empty to go back to `privatebin.net`.

The address is embedded in the links you create, so the people you share with reach the right server on their own. They do not need to change any setting.

## Host your own instance

PrivateBin is a small PHP application. The fastest setup is Docker:

```bash
docker run -d --name privatebin \
  -p 8080:8080 \
  -v privatebin-data:/srv/data \
  privatebin/nginx-fpm-alpine
```

Put it behind HTTPS with a reverse proxy such as Caddy or nginx. Point Opera at the HTTPS address and share as usual.

Requirements for the instance:

- It must run PrivateBin **v2** or later (the v2 API).
- HTTPS is strongly recommended; some browsers block mixed content on the web build.
- The instance's own retention policy applies. Opera asks for a three-day expiry, but the server may enforce a shorter or longer one.
