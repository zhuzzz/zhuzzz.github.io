---
layout: post
title: "Argo Workflow MCP Server In Golang"
date: 2025-05-03 23:59:59 +0800
categories: CATEGORY-1 CATEGORY-2
---

# Argo Workflow MCP Server In Golang

[github repo link](https://github.com/zhuzzz/argo-workflow-mcp-server/tree/main) 

## Support 3 Tools:
* get a specific workflow
* list workflows
* submit a workflow

## Testing in Claude Desktop

Testing environment: use kind with docker engine as container runtime to create a kubernetes cluster locally

![tools in Claude Desktop](/assets/argo-workflow-mcp-server-in-claude.png)
![submit a workflow in Claude Desktop](/assets/claude-argo-workflow-submit.png)

## Tool Name and Input
```
{
  "jsonrpc": "2.0",
  "id": 555,
  "result": {
    "tools": [
      {
        "annotations": {
          "destructiveHint": true,
          "openWorldHint": true
        },
        "description": "Get details of a specific workflow",
        "inputSchema": {
          "properties": {
            "name": {
              "description": "The name of the workflow",
              "type": "string"
            },
            "namespace": {
              "description": "The namespace of the workflow",
              "type": "string"
            }
          },
          "required": [
            "namespace",
            "name"
          ],
          "type": "object"
        },
        "name": "get_workflow"
      },
      {
        "annotations": {
          "destructiveHint": true,
          "openWorldHint": true
        },
        "description": "List all workflows in the cluster",
        "inputSchema": {
          "properties": {
            "namespace": {
              "description": "The namespace to list workflows from",
              "type": "string"
            }
          },
          "required": [
            "namespace"
          ],
          "type": "object"
        },
        "name": "list_workflows"
      },
      {
        "annotations": {
          "destructiveHint": true,
          "openWorldHint": true
        },
        "description": "Submit a new workflow",
        "inputSchema": {
          "properties": {
            "namespace": {
              "description": "The namespace to submit the workflow to",
              "type": "string"
            },
            "workflow_yaml": {
              "description": "The YAML definition of the workflow",
              "type": "string"
            }
          },
          "required": [
            "namespace",
            "workflow_yaml"
          ],
          "type": "object"
        },
        "name": "submit_workflow"
      }
    ]
  }
}
```


### callout
* proxy

    I have proxy setup in my local environment. Make sure to unset those envs when use kind to create cluster otherwise k8s cluster will use them and having problems pulling images

* make sure to pick the same yaml parser package used in argo codebase otherwise yaml parsing kept failing. don't use `gopkg.in/yaml.v3`