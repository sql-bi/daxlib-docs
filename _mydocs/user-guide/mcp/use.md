---
layout:         page
title:          Use the DAX Lib MCP Server
menu_title:     Use
published:      true
date:           2026-10-11
modified:       2026-11-01
order:          /user-guide/mcp/02
next_reading:   true
---

Write your requests to the assistant in natural language. The assistant selects the applicable [MCP tool](tools.md). This page shows typical workflows and example prompts.

## Typical workflow: install a package

1. **Find a package.** If you do not know the exact package id, ask the assistant to search DAX Lib.
2. **Select a package.** The assistant shows the results. You select the package.
3. **Examine the package.** Ask for the details or the README to see the functions and how to use them.
4. **Open your model.** Open the target model in Power BI Desktop. Make sure that the compatibility level is 1702 or higher.
5. **Select the target model.** The assistant lists the open Power BI Desktop instances. You select one, even if only one is open.
6. **Install the package.** Approve the install request in your MCP client.
7. **Save your file.** Save the file in Power BI Desktop. The server does not save it.

## Typical workflow: use functions in a DAX query

You can use the functions of a package in a DAX query without installing the package. The model does not change.

1. **Find a package.** Ask the assistant to search DAX Lib, then select the package.
2. **Get the functions.** Ask for the functions that you need. The server returns a `DEFINE` block with these functions and the functions that they call.
3. **Write the query.** Put the `DEFINE` block before `EVALUATE`, then run the query.

## Example prompts

### Search

- "Search DAX Lib for packages that generate SVG images."
- "Find DAX Lib packages for date calculations. Show only stable versions."
- "List all packages on DAX Lib."

### Examine a package

- "Show the details of DaxLib.SVG."
- "Which versions of DaxLib.SVG are available?"
- "Show the README of DaxLib.SVG."

### Install

- "List the Power BI Desktop models currently open."
- "Install DaxLib.SVG into the Sales Report model."
- "Install version 2.0.0 of DaxLib.SVG into the model on localhost:51542."

### Get functions for a DAX query

- "Give me the DEFINE block for DaxLib.SVG.Viz.Pill."
- "Get only DaxLib.SVG.Viz.Pill from DaxLib.SVG, without the functions it calls and without descriptions."
- "Get DaxLib.SVG.Viz.Pill and DaxLib.SVG.Viz.ProgressBar from DaxLib.SVG version 2.0.0. Tell me if the block is complete."
- "Write a DAX query that uses DaxLib.FormatString to format the sales amount by year. Do not install the package."

### Use the functions

After the installation, you can ask the assistant to help you use the functions. For example:

- "Using the README of DaxLib.SVG, write a measure that shows a bar for each product."

## Things to know

- **Versions.** If you do not specify a version, the server uses the latest published version. This version can be a prerelease. The assistant must tell you the version before it installs the package. To install a stable version, specify the version.
- **Replaced functions.** The installation replaces functions that have the same name. Other model objects do not change. A function in a `DEFINE` block replaces a model function with the same name only for that query.
- **Complete block.** If a called function is not in the `DEFINE` block, the result shows warnings and the block is not complete. Read the warnings before you run the query.
- **Reserved names.** Some functions published before a change of the DAX parser cannot run in a query, because a part of their name is now reserved. The query error shows the part of the name.
- **Approval.** The server does not ask for confirmation itself. Your MCP client asks you to approve the install tool call. Read the tool arguments before you approve.
- **Author content.** Package descriptions, release notes, and README files come from the package authors, not from DAX Lib. Examine them before you use the functions.
