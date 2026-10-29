---
title: FAQ
description: Short answers about accounts, models, privacy, sync and supported platforms.
---

## Is Opera free?

Opera is open source under the GNU AGPL v3. You can build it yourself and run it on your own hardware. Using a hosted model provider may cost money depending on that provider.

## Do I need an account?

No. Opera works without a sign-up. Sync is optional and can use a Sampler Hub, Nextcloud or Google Drive.

## Does it work offline?

Yes, with a downloaded on-device model or a local server on your network. A cloud provider naturally needs a connection.

## Where is my data stored?

Conversations and attachments live in the app's private SQLite storage. On-device models are local files. Nothing is uploaded unless you enable sync, a backup, sharing or a cloud provider.

## Which models can I use?

- Gemini Nano through Android AICore, or the browser's built-in model.
- On-device `.litertlm` models via LiteRT-LM.
- Ollama.
- Any OpenAI-compatible endpoint, including LM Studio and self-hosted gateways.

See [Models](/docs/guides/models/).

## What is the difference between Opera and Sampler Hub?

Opera is the assistant app. Sampler Hub is a self-hosted server for encrypted sync, profiles and shared local models. You can use Opera without a hub.

## Can I use Opera on several devices?

Yes. Pair them with a Sampler Hub, or move data with an encrypted cloud backup or a JSON export. See [Sync and sharing](/docs/guides/sharing/).

## Is sync end-to-end encrypted?

Sampler Hub sync is sealed end to end with the profile key. Nextcloud and Google Drive backups are encrypted with a PIN before upload. A JSON export is not encrypted by default.

## What happens if I forget my Sampler Hub password?

If no paired device remains, the profile cannot be decrypted. There is no account recovery. Keep a device paired or maintain a backup.

## Which platforms are supported?

Opera runs on Android, the web, and as Opera Desktop on Windows (x64 and ARM64), macOS (Apple silicon) and Linux (x86_64 and arm64). Sampler Hub runs on Windows, macOS (Apple silicon) and Linux (x86_64 and arm64). Check the releases page for the latest builds.

## Which languages does the interface support?

English and French.

## Can I turn tools off?

Yes. Every tool has its own toggle, and permissions are requested only when a feature needs them. A disabled tool is not offered to the model.

## How do I report a bug or contribute?

Open an issue or a pull request on [GitHub](https://github.com/MaestroAI-Company/opera). For Sampler Hub issues, use the [Sampler Hub repository](https://github.com/MaestroAI-Company/sampler-hub).

## Why is the first on-device reply slow?

The model has to load and warm up. Later replies in the same session are faster. A smaller model or a device with more memory will also help.
