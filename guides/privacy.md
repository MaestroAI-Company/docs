---
title: Privacy
description: What stays on your device, what syncs, and what leaves only when you choose it.
---

Opera is built around a simple rule: local by default, online only when you choose it. This page maps where data goes so you can decide what to enable.

## The short version

- No account is required.
- Chats, files and memory are stored in the app's private storage.
- A local model keeps prompts on the device.
- A cloud provider receives what you send while it is selected.
- PIN-encrypted cloud backups leave the device only as ciphertext; Sampler Hub sync is sealed with the profile key.
- Shared conversations are encrypted, and the key stays in the URL fragment.

## Data map

| Data | Where it lives | Leaves the device? |
| --- | --- | --- |
| Conversations | SQLite database in the app's private storage | Only with cloud sync, backup or sharing |
| Settings and provider keys | App storage | Encrypted with sync or backup |
| Attachments | App storage | Only to the provider you send them to |
| On-device models | Local storage | No |
| Incognito chats | Memory only | Only to the selected provider |
| Sampler Hub sync records | Sampler Hub's SQLite database | Sealed end to end with the profile key |
| Web search queries | DuckDuckGo | Yes, when web search is enabled |

## Cloud providers

When you choose an online model, the prompt and any attachments needed for the answer are sent to that provider. Opera does not add analytics or a proxy in the middle. The provider's own retention policy applies.

Use a local model, an Ollama server, or an OpenAI-compatible endpoint on your own network when the content must not leave your infrastructure.

## Incognito mode

Incognito conversations are never written to history. They still use whichever provider is selected, so the provider can receive the content while it answers. Incognito protects local history, not the network.

## Sync and backups

Opera supports:

- **Nextcloud or Google Drive sync**: encrypted with a PIN before upload.
- **Local JSON export and import**: useful for manual backups and migration.
- **Sampler Hub**: end-to-end encrypted sync between paired devices.

For PIN-encrypted sync, the PIN is not stored on the server. Losing it means losing access to the encrypted data. For Sampler Hub profiles, the profile key is created on the device and never reaches the hub in clear.

## Sharing

Conversations are shared as encrypted [PrivateBin](https://privatebin.info) links. The decryption key is kept in the URL fragment, which browsers do not send to the server. The PrivateBin instance is configurable.

Treat a share link like the conversation itself: anyone with the full link can read it.

## Web search and tools

Web search uses DuckDuckGo and only runs when the tool is enabled and the model calls it. Page fetching, clipboard access, contacts, calendar, messages and screen capture are separate tools with their own toggles.

Every tool can be disabled. A disabled tool is not offered to the model.

## Deleting data

- Delete a conversation from history to remove it from the local database.
- Delete on-device models from settings to reclaim storage.
- Remove a provider to delete its stored key.
- Unpair a device from Sampler Hub to cut off its access immediately.
- Removing a Sampler Hub profile deletes its data, devices and MCP servers from the hub.

:::note
Backups and sync copies are separate from the local database. Deleting a conversation locally does not automatically delete an existing encrypted backup. Remove the backup or overwrite it if you need a full wipe.
:::
