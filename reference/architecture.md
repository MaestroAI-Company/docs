---
title: Architecture
description: How the app, providers, storage, native modules and Sampler Hub fit together.
---

Opera is a single Expo application that targets Android, the web and a Tauri desktop shell. The same TypeScript code drives the chat interface, provider layer and local storage on every platform; native code is used only where a platform capability requires it.

## Stack

| Layer | Technology |
| --- | --- |
| Mobile / web UI | Expo SDK 57, React Native, `expo-router`, React 19 |
| Local database | SQLite via `expo-sqlite` |
| On-device AI | LiteRT-LM, Android AICore (Gemini Nano), ExecuTorch for object detection |
| Speech | System speech recognizer, Whisper via `@xenova/transformers` on web |
| Native Android | Kotlin / Java: voice interaction, overlay, screen capture, text selection, AICore bridge |
| Crypto | `react-native-quick-crypto` / WebCrypto |
| Desktop shell | Tauri |
| Language | TypeScript, strict |

## The request path

A message moves through a small number of layers:

1. **UI**: the chat screen collects text, attachments and tool choices.
2. **Generation pipeline**: builds the conversation context, resolves mentions, selects the provider and streams the reply.
3. **Provider**: built-in, on-device, Ollama or OpenAI-compatible. Each provider adapts the common request to its own API.
4. **Tools**: if the model calls a tool, the pipeline executes it, returns the result and continues generation.
5. **Storage**: the conversation is written to SQLite unless incognito is active.

Keeping providers behind one interface is what lets a conversation switch models without changing the rest of the app.

## Providers

- **Built-in**: Gemini Nano through Android AICore, or the browser's built-in model on web.
- **On-device**: `.litertlm` models run through LiteRT-LM.
- **Ollama**: an HTTP provider pointed at an Ollama server.
- **OpenAI-compatible**: any chat-completions endpoint, including LM Studio and self-hosted gateways.

Provider credentials live with the provider configuration. They are included in encrypted sync and backups, not in plaintext exports unless you export them deliberately.

## Storage

Conversations, messages, settings and provider configurations live in a SQLite database in the app's private storage. Attachments are stored alongside it. On-device models are separate files and can be removed independently.

Incognito conversations bypass history writes. They can still use any provider, including a cloud one.

## Native Android modules

The Android build includes Kotlin/Java modules for capabilities the web runtime cannot provide:

- the voice interaction service for the assistant role;
- the overlay that draws over other apps;
- screen capture, on-screen text selection and object detection;
- the AICore bridge for Gemini Nano.

These are exposed to TypeScript through native modules and are optional at runtime. A missing permission disables the feature, not the app.

## Crypto and sync

- PIN-encrypted Nextcloud and Google Drive backups use WebCrypto or `react-native-quick-crypto`.
- Shared conversations use PrivateBin with the key in the URL fragment.
- Sampler Hub seals every synced record with the profile key using XChaCha20-Poly1305.
- Sampler Hub pairing stretches the one-time code with Argon2id; device links use X25519 with a commitment.
- Sampler Hub storage encrypts each row again with XChaCha20-Poly1305 and keeps the key in the OS keychain or a key file.

## Sampler Hub transport

Devices reach the hub through [iroh](https://github.com/n0-computer/iroh) QUIC connections. Connections are encrypted end to end and authenticated by key. Devices connect directly when possible and through a relay otherwise, so the hub works without opening a port.

Every request is denied by default. Access is checked again on every stream, so removing a device cuts it off immediately.

## Project layout

```text
src/
  app/                 expo-router screens
  components/          feature UI, design-system primitives, widgets
  services/
    ai/                providers, tools, generation, mentions
    mcp/               MCP client, OAuth, server storage
    cloud/, crypto/    sync providers and encrypted backup
    db/                SQLite-backed conversation storage
    speech/            STT / TTS
    overlay/           screen capture and selection
    documents/         PDF / DOCX extraction
    share/             PrivateBin links
  i18n/                English and French catalogs
native/android/        Kotlin/Java modules
src-tauri/             desktop shell
```

## License

Opera and Sampler Hub are licensed under the GNU AGPL v3. If you run a modified version of Opera as a network service, you must make your source available too.
