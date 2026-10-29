---
title: Tools and MCP
description: Connect calendars, files, search and custom Model Context Protocol servers.
---

Opera can call tools during a conversation: search the web, fetch a page, do math, read the clipboard, open apps, send messages, look up contacts, read the calendar, set alarms, and open Android settings panels. Each tool can be switched on or off.

For anything else, connect a [Model Context Protocol](https://modelcontextprotocol.io) server. MCP is an open protocol for exposing tools and data to AI clients. Opera supports OAuth-aware MCP servers, and their tools appear in chat.

## Built-in tools

![Opera tool details](../images/tool-info.png)

| Tool | What it does |
| --- | --- |
| Web search | Searches DuckDuckGo |
| Page fetch | Reads a web page and returns its content |
| Math | Evaluates calculations |
| Clipboard | Reads or writes the clipboard |
| Open app | Launches an installed app |
| Send message | Composes a message in a messaging app |
| Contacts | Looks up contact details |
| Calendar | Reads and creates events |
| Alarms | Creates alarms and timers |
| Settings panels | Opens Android settings screens |

Tools are opt-in at the point of use. A tool that is disabled is not offered to the model, and a permission you have not granted blocks the related tool.

## Add an MCP server

MCP servers are managed from Opera's settings. The exact fields depend on the server, but the flow is:

1. Open **Settings → Tools & MCP**.
2. Add a server with its name and endpoint.
3. Complete OAuth if the server requires it.
4. Enable the tools you want the model to see.

Once connected, tools can be referenced directly in a message with an `@mention`. This is useful when you want a specific tool rather than letting the model choose.

```text
@calendar what does my week look like?
```

:::tip
Give servers descriptive names. When several tools overlap, the name and description are what the model uses to choose between them.
:::

## Hosted MCP servers on the hub

Members of a Sampler Hub can install and run their own MCP servers on the hub. A member's servers only reach that member's folder on the hub, never the host's files. This keeps a shared hub useful without turning it into a shared filesystem.

## Security

- Treat an MCP server as code you are choosing to trust. It can see the inputs the model sends it.
- Prefer servers you host yourself, or ones with a clear data policy.
- Review OAuth scopes before approving a connection.
- Disable a server you no longer use; removing it also removes its stored credentials.
- Tools that touch messages, contacts or the screen are the most sensitive. Enable them only when a workflow needs them.

:::caution
Prompt injection is a real risk with any tool that reads untrusted content, such as a fetched web page. A page can contain instructions aimed at the model. Keep high-impact tools off during exploratory browsing.
:::

## Troubleshooting

**A server connects but no tools appear.** Check that the server exposes tools, that OAuth completed, and that the tools are enabled in Opera.

**A tool works on one device but not another.** Permissions and provider settings are per device. Check the permission and the selected model's tool support.

**The model ignores an `@mention`.** Not every model handles mentions equally well. Try a more explicit prompt or a model with stronger instruction following.
