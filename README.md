# PlanetScale MCP Registry Entry

This repository contains the [`server.json`](./server.json) metadata file used to publish the [PlanetScale MCP server](https://planetscale.com/docs/connect/mcp) to the [MCP Registry](https://registry.modelcontextprotocol.io).

## What is this?

The MCP Registry is a public directory of MCP (Model Context Protocol) servers. It allows tools like Cursor, Claude, VS Code, and others to discover and connect to MCP servers.

This repo holds the registry entry for PlanetScale's hosted MCP server at `https://mcp.pscale.dev/mcp/planetscale`. The actual server code lives in [planetscale/mcp-server](https://github.com/planetscale/mcp-server).

## Publishing

The registry entry is published using the [`mcp-publisher`](https://github.com/modelcontextprotocol/registry) CLI tool.

### First-time setup

1. Install `mcp-publisher` (via Homebrew or from the registry repo):
   ```bash
   brew install mcp-publisher
   ```

2. Authenticate with GitHub (your PlanetScale org membership must be **public**):
   ```bash
   mcp-publisher login github
   ```

### Validate and publish

```bash
mcp-publisher validate
mcp-publisher publish
```

### Why is GitHub authentication required?

The registry uses GitHub authentication to verify that the person publishing under `io.github.planetscale/*` is actually a member of the `planetscale` GitHub org. This prevents anyone else from registering a server under PlanetScale's name. It has no relation to the OAuth flow that end users go through when connecting to the PlanetScale MCP server.

## Updating the entry

Edit `server.json`, bump the `version` field, then run `mcp-publisher publish`. Consider adding a GitHub Actions workflow to automate this on merge -- see the [registry CI/CD docs](https://github.com/modelcontextprotocol/registry/blob/main/docs/modelcontextprotocol-io/github-actions.mdx) for a ready-made workflow.
