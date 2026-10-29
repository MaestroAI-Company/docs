---
title: Desktop
description: Run Opera on the desktop, in the browser, or host a Sampler Hub from the desktop app.
---

Opera Desktop brings Maestro to your computer, on Windows, macOS and Linux. It can also host a Sampler Hub for your other devices, and keep your conversations, settings and providers in sync with them.

## Install a release

Download your build from the [download page](https://maestroai.company/opera#download) or from the [latest Opera release](https://github.com/MaestroAI-Company/opera/releases/latest):

| Platform | File | Install |
|---|---|---|
| Windows x64 | `opera-windows-x86_64-setup.exe` | Run the installer. It installs for your user only, no administrator rights needed. |
| Windows ARM64 | `opera-windows-aarch64-setup.exe` | Same installer, built for Snapdragon and other ARM PCs. |
| macOS (Apple silicon) | `opera-macos-aarch64.dmg` | Open the disk image and drag Opera to **Applications**. |
| Linux x86_64 | `opera-linux-x86_64.AppImage` or `.deb` | Make the AppImage executable and run it, or install the package with `sudo apt install ./opera-linux-x86_64.deb`. |
| Linux arm64 | `opera-linux-aarch64.AppImage` or `.deb` | Same as x86_64. |

:::note
The builds are not signed yet. Windows SmartScreen may ask you to confirm with **More info → Run anyway**, and macOS may need a right-click → **Open** the first time.
:::

If a build is not available for your platform, run Opera in the browser or build it from source.

## Run from source

You need Node.js and npm. A Rust toolchain is only required for the Tauri desktop shell, which also builds against a [Sampler-Hub](https://github.com/MaestroAI-Company/Sampler-Hub) checkout placed next to the Opera repository.

```bash
npm install
npm start
```

From the Expo dev server you can:

- press `w` to open the web build;
- press `a` for Android.

```bash
npm run web
npm run desktop         # Opera Desktop against the dev server
npm run build:desktop   # installer for the current machine
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
- **Updates.** Opera checks the latest GitHub release and shows a notice at the top of **Settings** when a newer version is out. Install it over the current one, your data is kept. On the first launch after an update, a **What's new** sheet shows the release notes. Source builds update with `git pull` and a rebuild.

:::caution
If you use a cloud provider on desktop, the provider receives the conversation content needed to answer. Use a local model or incognito mode when that is not acceptable.
:::
