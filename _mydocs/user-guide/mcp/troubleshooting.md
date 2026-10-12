---
layout:         page
title:          Troubleshoot the DAX Lib MCP Server
menu_title:     Troubleshooting
published:      true
date:           2026-10-11
modified:       2026-10-11
order:          /user-guide/mcp/04
next_reading:   true
---

## Find the server output

The server writes diagnostic messages to the output of your MCP client. The messages stay on your computer.

In VS Code:

1. Open the Command Palette.
2. Run **MCP: List Servers**.
3. Select the DAX Lib MCP server.
4. Select **Show Output**.

In the Code tab of the Claude application or in Claude Code, run `/mcp` to see the status of the server. If the server is not in the list, make sure that the entry is at the top level of `%USERPROFILE%\.claude.json`, then restart the application.

In the Chat tab of the Claude application, the MCP logs are in `%APPDATA%\Claude\logs`. The file `mcp-server-daxlib-mcp.log` contains the output of the server, if the server name in the configuration is `daxlib-mcp`.

In Cursor, open the **Output** panel and select **MCP Logs**.

Do the failed action again, then read the most recent messages.

To collect a detailed diagnostic trace, refer to [Troubleshooting DAX Lib MCP](https://github.com/daxlib/daxlib-mcp/blob/main/docs/troubleshooting.md) in the daxlib-mcp repository.

## The server does not start

| Problem | Solution |
|---|---|
| The message says that the platform package `@daxlib/mcp-<platform>-<arch>` is not installed. | The server runs only on Windows x64. On a supported platform, run `npm install @daxlib/mcp-win32-x64`, then try again. |
| `npx` is not found. | Install Node.js version 18 or higher. Restart the MCP client after the installation. |
| The message mentions `npx` or `spawn`. | Use `cmd` as the command, with the arguments `/c`, `npx`, `-y`, `@daxlib/mcp`, and `--start`. On Windows, `npx` is a `.cmd` script, and some clients cannot start it without a shell. |
| The server is not shown in the client. | Make sure that the JSON configuration is correct. Make sure that you use the correct key (`mcpServers` or `servers`) for your client. Restart the client. |

To test the server outside the client, run `npx -y @daxlib/mcp --version` in a terminal.

## Search and package errors

| Message | Cause and solution |
|---|---|
| No packages matched the query. | The query is matched as one substring. Use one keyword, for example `svg`, `date`, or `format`. If you excluded prereleases, include them. |
| No DAX Lib package with this id exists. | The package id is not correct. The message can show possible matches. Use `search_packages` to find the correct id. |
| The package does not have this version. | The message shows the available versions. Use one of them. |
| The package version does not have a README. | The author did not publish a README for this version. |

## Installation errors

| Message | Cause and solution |
|---|---|
| The `dataSource` does not match any local Power BI Desktop instance. | The instance is closed, or the value is not correct. Ask the assistant to list the open instances again, then select one. |
| The connection to the instance could not be established. | Make sure that Power BI Desktop is open and that the model is loaded. Try again. |
| The model's compatibility level is lower than 1702. | User-defined functions need compatibility level 1702 or higher. The DAX Lib MCP server does not change the compatibility level. Raise it yourself, then install the package again. Refer to [Raise the compatibility level](#raise-the-compatibility-level). |
| The instance hosts a number of databases different from one. | The model is not loaded. Open the target model in Power BI Desktop, then try again. |
| The package could not be read. | The package content is not valid. Do not try again. Report the problem to the package author. |
| The engine could not save the change. | Power BI Desktop rejected the change. Read the error message. Do not try again automatically. |

## Raise the compatibility level

You can use the [Power BI Authoring MCP server](https://learn.microsoft.com/en-us/power-bi/developer/mcp/power-bi-authoring-mcp) ([GitHub repository](https://github.com/microsoft/powerbi-modeling-mcp)) to raise the compatibility level to 1702 or higher. Suggested prompt:

```text
Connect to the model open in Power BI Desktop and make sure that the compatibility level is at least 1702.
```

## The installed functions are not saved

The server changes the model in Power BI Desktop, but it does not save the file. Save the file in Power BI Desktop.

## Report a problem

To report a problem with the MCP server, [open an issue on GitHub](https://github.com/daxlib/daxlib-mcp/issues/new). Include the server version (`npx -y @daxlib/mcp --version`), your MCP client, and the messages from the server output.
