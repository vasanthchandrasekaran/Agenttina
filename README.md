# Avaniko plugin marketplace

This repo is a Claude plugin marketplace. It indexes plugins built by Avaniko for B2B sales, finance, and operations teams.

## Plugins

| Plugin | Description |
|--------|-------------|
| **avaniko-agent-tina** | Sales co-pilot — pipeline review, account research, call prep, outreach drafting, autonomous deal-health scoring |

## Install

After this repo is published to GitHub, anyone with Claude Code can add it as a marketplace and install plugins from it:

```bash
# Add this marketplace
claude plugin marketplace add <github-user>/avaniko-marketplace

# Browse what's available
claude plugin marketplace list

# Install Agent Tina
claude plugin install avaniko-agent-tina@avaniko
```

## Repo layout

```
avaniko-marketplace/
├── .claude-plugin/
│   └── marketplace.json     # marketplace index
├── plugins/
│   └── avaniko-agent-tina/  # the plugin itself
└── README.md
```

Each entry in `marketplace.json` points at a subdirectory under `plugins/` that contains a valid plugin (with its own `.claude-plugin/plugin.json`).

## Submitting to Anthropic's official directory

To get listed in Anthropic's curated plugin marketplace (so users don't need to add the marketplace by URL), follow Anthropic's submission process at <https://docs.claude.com/claude-code/plugins>. The same `marketplace.json` is used.

## License

MIT
