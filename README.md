# Airframe Claude plugin marketplace

This directory is the source for the **public `airframeai/claude-plugin`
marketplace repository** — the org-installable bundle that ships the Airframe
MCP connector together with the `company-research` skill to Claude Cowork and
Claude Code users. It lives in the monorepo so it versions alongside the
mcp-server it fronts; publishing is a copy of this directory to the public
repo root (the marketplace layout requires `.claude-plugin/marketplace.json`
at the repository root).

## Layout

```
.claude-plugin/marketplace.json      # marketplace manifest (lists the plugins below)
plugins/airframe/
  .claude-plugin/plugin.json         # plugin manifest
  .mcp.json                          # registers the remote Airframe MCP server
  skills/company-research/SKILL.md   # routing playbook + brief format
```

The plugin contains **no server code** — the MCP server is remote
(`https://mcp.airframe.ai/mcp`, streamable HTTP + OAuth). Tool changes deploy
server-side and reach users instantly; only *skill* changes require a plugin
version bump here and a re-publish.

## What the plugin adds over the bare connector

The connector alone (installed from the Anthropic connector directory or by
URL) already carries the steering that matters most: trigger-rich tool
descriptions and server-level routing instructions (`mcp_server/main.py`).
The plugin layers on:

- the `company-research` skill — a deterministic routing playbook, a
  consistent brief/battlecard output format, and a "never answer vendor
  questions from memory" policy;
- one-step install of connector + skill together, org-deployable.

## How customers install it

**Org-wide (Claude Cowork / Claude Desktop)** — an org admin adds the
published repo to `allowedPluginMarketplaces` (MDM or managed config). The
plugin then appears under *Settings → Plugins → Organization* for every seat;
the admin can mark it auto-install. Requires Claude Desktop 1.17377.1+.

**Org-wide (Claude Code)** — the same repo goes in `extraKnownMarketplaces`
in `managed-settings.json`.

**Per-user (either product)** — Claude Code:
`/plugin marketplace add airframeai/claude-plugin`, then
`/plugin install airframe@airframe`. Cowork: *Customize → Plugins*.

## Publishing checklist

1. Bump `version` in `plugins/airframe/.claude-plugin/plugin.json` (and the
   marketplace `metadata.version` if the manifest itself changed).
2. Copy this directory's contents to the public `airframeai/claude-plugin`
   repo root and push.
3. Sanity-check locally first: `claude` → `/plugin marketplace add
   /path/to/this/directory` → `/plugin install airframe@airframe` → confirm
   the `company-research` skill loads and the `airframe` server connects.

Keep this bundle free of anything internal: it is written for external
customers, so no references to internal tools, devbox URLs, or the local
docker stack.
