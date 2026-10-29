---
title: Desktop
description: Run Opera on the desktop, in the browser, or host a Sampler Hub from the desktop app.
---

Opera's interface is shared between Android and the web. The desktop build wraps the same app in a Tauri shell, so conversations, settings and providers stay consistent across platforms.

## Install a release

Download the latest desktop build from the [Opera releases page](https://github.com/MaestroAI-Company/opera/releases). If a build is not available for your platform yet, run Opera in the browser or build it from source.

## Run from source

You need Node.js and npm. A Rust toolchain is only required for the Tauri desktop shell.

```bash
npm install
npm start
```

From the Expo dev server you can:

- press `w` to open the web build;
- press `a` for Android;
- open the desktop shell with the Tauri command configured in the repository.

```bash
npm run web
```

The web build runs in any modern browser. On the web, Opera can use the browser's built-in model, a remote OpenAI-compatible endpoint, or Whisper for local speech recognition.

## Host Sampler Hub from desktop

The desktop app can run a Sampler Hub without a separate installation:

1. Open **Settings → Sampler Hub**.
2. Choose **Host the hub here**.
3. Pair your phone or browser with the code shown by the app.

This is the quickest way to try sync and shared models. For an always-on hub, install the standalone service instead: [Sampler Hub](/docs/install/hub/).

## Desktop behaviour

- **Local storage.** The desktop shell uses the same SQLite-backed store as the app. Your data stays in the app's data directory.
- **Local providers.** Ollama and OpenAI-compatible servers are reached over the network you configure. A local server on the same machine is the lowest-latency option.
- **Updates.** Release builds check for updates through the distribution channel. Source builds update with `git pull` and a rebuild.

:::caution
If you use a cloud provider on desktop, the provider receives the conversation content needed to answer. Use a local model or incognito mode when that is not acceptable.
:::
