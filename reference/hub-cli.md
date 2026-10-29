---
title: Sampler Hub CLI
description: Commands for running, pairing, managing and servicing a Sampler Hub.
---

The `sampler-hub` binary runs the hub, manages devices and profiles, and installs itself as a background service. Run `sampler-hub --help` for the full command list.

## Commands

| Command | What it does |
| --- | --- |
| `sampler-hub run` | Run the hub in the foreground |
| `sampler-hub pair` | Show a one-time QR code and code to pair a device |
| `sampler-hub devices` | List paired devices |
| `sampler-hub devices remove <id>` | Unpair a device by id or id prefix |
| `sampler-hub profiles` | List profiles |
| `sampler-hub profiles remove <id>` | Remove a profile with its data, devices and MCP servers |
| `sampler-hub profiles promote <id>` | Let a profile manage the hub |
| `sampler-hub service install` | Start the hub with your session, now and at every login |
| `sampler-hub service start` | Start the background service |
| `sampler-hub service stop` | Stop the background service |
| `sampler-hub service status` | Show the service status |
| `sampler-hub service uninstall` | Stop the hub and remove it from your session |
| `sampler-hub ticket` | Print the hub ticket and its QR code, for `ping` |
| `sampler-hub ping <ticket>` | Check that a hub is reachable |

Every command accepts `--data-dir <path>` to use another data directory, for example to run two hubs side by side.

## Pairing

```sh
sampler-hub pair
```

The code is valid for a single pairing. On the same network, Opera also discovers the hub automatically, but the code is still required. A wrong code closes the pairing endpoint after five attempts.

## Devices

```sh
sampler-hub devices
sampler-hub devices remove 7f3a
```

Removing a device revokes its key. Access is checked again on every stream, so a removed device is cut off immediately rather than at the next restart.

## Profiles

```sh
sampler-hub profiles
sampler-hub profiles promote 2c9e
sampler-hub profiles remove 2c9e
```

The first profile manages the hub; promoted profiles become admins. Removing a profile deletes its data, devices and hosted MCP servers from the hub.

:::danger
Profile removal is irreversible. A profile with no remaining device and a forgotten password cannot be recovered.
:::

## Service management

On Linux and macOS, the installer registers a user service. On Windows, the installer starts the hub with your session.

```sh
sampler-hub service status
sampler-hub service stop
sampler-hub service start
sampler-hub service uninstall
```

## Reachability

```sh
sampler-hub ticket
sampler-hub ping <ticket>
```

`ticket` prints the hub ticket and `ping` checks that a hub is reachable with it. This is useful when debugging a pairing or a relay connection.

## Data directories

| OS | Data directory |
| --- | --- |
| Windows | `%LOCALAPPDATA%\MaestroAI-Company\Sampler-Hub\data` |
| macOS | `~/Library/Application Support/company.MaestroAI-Company.Sampler-Hub` |
| Linux | `~/.local/share/samplerhub` |

## Build

```sh
cargo build --release -p sampler-hub                         # sampler-hub and sampler-hubw, the tray app
cargo build --release -p sampler-hub --no-default-features   # sampler-hub only, for headless servers
cargo test --workspace
```

The workspace contains four crates:

| Crate | Role |
| --- | --- |
| `sampler-hub` | CLI, background service, tray, sync store, llama.cpp runtime |
| `sampler-hub-proto` | Protocol types shared by the hub and clients |
| `sampler-hub-client` | Client library with Kotlin and WebAssembly bindings |
| `uniffi-bindgen` | Generates the Kotlin bindings |
