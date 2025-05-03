---
layout: post
title: "Yannan First Blog"
date: 2025-03-16 10:00:00 +0800
categories: CATEGORY-1 CATEGORY-2
---

# MCP and Tool Use Note

Model Context Protocol

cursor
	browser tool MCP server - can actually check chrome console log


## MCP vs Tool Use

Tool Use

* Claude does not have access to built-in server-side tools 
* Claude isn't running code on its own
* User provides the tools in each API request. Users define the tools with descriptions/input schemas/implementations and executes the tool logic

![MCP calling trace](/assets/Tool-Use-drawing.png)


**Why MCP is better than existing tools use(function calling)?**
1. for function calling, function definition/implementation is done at client's side. Lots of boilerplate  code needs to be written for a model to use tools. Function execution is at client's side too. 
2. for MCP, function definition/implementation/execution is done at MCP server side. Only write function implementation once.