---
layout:         page
title:          Use DAX Lib with AI Assistants (MCP)
menu_title:     AI Assistants (MCP)
published:      true
date:           2026-10-11
modified:       2026-10-11
order:          /user-guide/03
next_reading:   true
---

The DAX Lib MCP server connects an AI assistant to DAX Lib. MCP (Model Context Protocol) is an open standard that lets an assistant use external tools. Examples of MCP clients are Claude Desktop, GitHub Copilot in VS Code, and Cursor.

## Supported clients

We tested the server with these MCP clients: Claude (Claude Desktop and Claude Code), GitHub Copilot in VS Code, and Codex. This list can change. We expect the server to work with all MCP clients that support local (stdio) servers. If you find a problem with a client, [open an issue on GitHub](https://github.com/daxlib/daxlib-mcp/issues).

## What the server does

With the DAX Lib MCP server, you can ask your assistant to:

- Search the DAX Lib catalog for packages.
- Show the details, versions, and README of a package.
- List the Power BI Desktop models that are open on your computer.
- Install the functions of a package into a model open in Power BI Desktop.

The server is distributed as the npm package [@daxlib/mcp](https://www.npmjs.com/package/@daxlib/mcp). It runs locally on your computer. It does not need a configuration file, environment variables, or API keys. The source code is in the [daxlib-mcp repository](https://github.com/daxlib/daxlib-mcp) on GitHub.

## How the installation works

When you install a package, the server does these steps:

1. It downloads the package from DAX Lib.
2. It connects to the model that you selected.
3. It makes sure that the model compatibility level is 1702 or higher.
4. It adds the user-defined functions of the package to the model. If a function with the same name exists, the server replaces it.

The server does not change other model objects. The package code does not go through the assistant, so the server installs the functions with their original formatting and comments.

> The server does not save your Power BI Desktop file. After the installation, save the file in Power BI Desktop to keep the changes.

## You stay in control

- You select the package and the version. The server instructs the assistant to let you choose and not to select a package automatically.
- You select the target model. The assistant must use a model from the list of open Power BI Desktop instances.
- The install tool is marked as a tool that changes data. Most MCP clients ask for your approval before they run it.

## Limits

- The server runs only on Windows x64. There are no plans for a macOS version at this time. If you want a macOS version, [tell us in a GitHub issue](https://github.com/daxlib/daxlib-mcp/issues/new).
- You can install packages only into models open in Power BI Desktop on the same computer.
- The server does not remove or update installed functions. To update a package, install the new version. The server replaces functions with the same name.

## Pages in this section

- [Install the MCP server](install.md)
- [Use the MCP server](use.md)
- [MCP tools reference](tools.md)
- [Troubleshoot the MCP server](troubleshooting.md)
