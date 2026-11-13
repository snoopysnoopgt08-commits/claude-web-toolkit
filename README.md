# claude-web-toolkit

My Claude Code toolkit for building websites, packaged as a plugin so it works in **every project** on any device.

## What's inside

- **12 skills:** banner-design, brand, core-web-vitals-auditor, design, design-system, frontend-design, impeccable, shopify-theme-architect, slides, ui-styling, ui-ux-pro-max, wordpress-block-engine
- **4 agents:** impeccable-asset-producer, impeccable-documenter, impeccable-finish-reviewer, impeccable-manual-edit-applier
- **2 MCP servers:** shadcn, magicuidesign-mcp

## Install on a device (once)

In Claude Code:

```
/plugin marketplace add snoopysnoopgt08-commits/claude-web-toolkit
/plugin install web-toolkit@claude-web-toolkit
```

The repo is private, so that device's git must be logged in to GitHub with access to it.

Restart Claude Code. The skills, agents and MCP servers are then available in every project.

## Update

Change a skill here, raise `version` in `.claude-plugin/plugin.json`, commit and push. On each device: `/plugin marketplace update claude-web-toolkit`, then update the plugin from `/plugin`.

## Not included on purpose

- **21st.dev MCP** needs a personal API key. Add it per device:
  `claude mcp add --transport http --scope user 21st https://21st.dev/api/mcp --header "x-api-key: <your key>"`
- **filesystem / git MCP** were tied to one PC's folders, and Claude Code already reads files and runs git itself.

## Notes

- `.mcp.json` starts the servers with `cmd /c npx` (Windows). On macOS/Linux use `"command": "npx"` and drop `cmd` and `/c`.
- `ui-ux-pro-max` needs Python 3 for its search script.
- Some skills (impeccable, ui-ux-pro-max and others) come from third parties. Keep this repo private unless their licences allow sharing.
