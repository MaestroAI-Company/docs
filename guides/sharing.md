---
title: Sync and sharing
description: Move conversations between devices, back them up, and share them safely.
---

Opera gives you several ways to move data. They have different trust models, so pick the one that matches the job.

## Compare the options

| Method | What moves | Encryption | Best for |
| --- | --- | --- | --- |
| **Sampler Hub** | Conversations, settings, providers, models | End to end, per profile | A set of devices you own |
| **Nextcloud / Google Drive** | Conversations and settings | PIN-encrypted before upload | An existing cloud account |
| **JSON export** | A local snapshot | None by default | Manual backups and migration |
| **PrivateBin link** | One conversation | Encrypted, key in the URL fragment | Sending a chat to someone |

## Sampler Hub

Sampler Hub is the most complete option. Pair a phone, desktop and browser, then choose what each device syncs. Records are sealed on the device with the profile key before they reach the hub, so the hub stores ciphertext.

- Pairing uses a one-time QR code or 8-character code.
- Each device has its own key and permissions.
- Removing a device cuts off access on the next request.
- Admin profiles can manage devices and updates from Opera.

Read [Install Sampler Hub](/docs/install/hub/) for setup.

## Nextcloud and Google Drive

Opera can sync an encrypted backup to Nextcloud or Google Drive. The backup is encrypted with a PIN before it leaves the device.

- Use a PIN you can remember; there is no server-side reset.
- The cloud provider stores ciphertext, but it can still see when backups happen and how large they are.
- Restoring on a new device requires the same PIN.

## JSON export and import

Export writes a local JSON snapshot. This is useful before a reset, before a migration, or as a second copy.

```text
Settings → Data → Export
```

:::caution
A JSON export is not encrypted by default. Store it somewhere you trust, and delete it when you no longer need it.
:::

## Share a conversation

Opera shares conversations as encrypted PrivateBin links:

1. Open the conversation menu.
2. Choose **Share**.
3. Pick a PrivateBin instance if you do not want the default.
4. Send the generated link.

The decryption key is kept in the URL fragment (`#...`), which is not sent to the server in an HTTP request. The server stores encrypted content and cannot read it.

Anyone with the complete link can read the conversation. Do not post a share link publicly if the chat contains personal data.

## Backups and deletion

- A sync copy is not the same as a local conversation. Deleting locally does not remove an existing backup.
- To fully wipe a synced account, delete the local data, remove the cloud backup, and remove the device from Sampler Hub.
- For Sampler Hub profiles, removing the profile deletes its data, devices and MCP servers from the hub.

## Moving to a new phone

1. Export a JSON backup or make sure Sampler Hub sync is current.
2. Install Opera on the new device.
3. Restore the backup, or pair the new device with Sampler Hub and choose the existing profile.
4. Check providers and permissions; these can differ between devices.
5. Remove the old device from Sampler Hub when you are sure the move is complete.
