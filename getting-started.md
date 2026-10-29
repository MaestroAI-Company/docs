---
title: Getting started
description: Install Opera, choose a model and have your first private conversation.
---

Opera is a privacy-first AI assistant. You can run a model on the device itself, connect your own Ollama server, or use any OpenAI-compatible endpoint. There is no account, and nothing leaves your device unless you choose an online model, cloud sync or web search.

## What you need

- An Android phone or tablet, a desktop computer, or a modern browser.
- For on-device models: enough free storage and memory for the model file you want to run.
- For Ollama or another local server: the server running on a machine Opera can reach.
- For an online provider: an API key from that provider.

:::note
Opera is in beta. Features and screens may change between builds, especially around the hub and on-device models.
:::

## Install Opera

| Platform | Where to start |
| --- | --- |
| Android | [Join the beta or build a dev client](/docs/install/android/) |
| Desktop | [Download a release or build from source](/docs/install/desktop/) |
| Browser | Open the web build from the Opera site, or run it locally with `npm run web` |
| Your own server | [Install Sampler Hub](/docs/install/hub/) for sync and shared models |

## First run

1. **Choose a provider.** Pick a built-in model, an on-device model, Ollama, or an OpenAI-compatible endpoint.
2. **Download a model if needed.** On-device models are stored locally and survive app updates. You can remove them later from settings.
3. **Grant only the permissions you want.** Camera, microphone, contacts, calendar and screen access are optional and can be toggled individually.
4. **Send a message.** Ask a question, attach a PDF, or use the microphone.

If you want Opera to replace Google Assistant, set it as the default assistant. This is optional and can be reversed at any time.

## Keep it private

Opera's defaults are local-first:

- Conversations are stored in the app's private SQLite database.
- Incognito conversations are never written to history.
- Cloud providers only receive the messages you send while they are selected.
- Cloud backups are encrypted with a PIN; Sampler Hub sync is sealed with the profile key.
- Shared conversations use encrypted PrivateBin links, with the key kept in the URL fragment.

Read [Privacy](/docs/guides/privacy/) for the full data map.

## Where to go next

- [Choose a model](/docs/guides/models/)
- [Connect tools with MCP](/docs/guides/mcp/)
- [Use Opera as a voice assistant with Stand-by](/docs/guides/standby/)
- [Sync between devices with Sampler Hub](/docs/install/hub/)
- [Understand the architecture](/docs/reference/architecture/)
