# Codex Exa

English | [简体中文](README.zh-CN.md)

A Git-backed Codex Marketplace for current web search and full-page retrieval through the official [Exa MCP](https://github.com/exa-labs/exa-mcp-server) service.

> This is a community-maintained integration and is not an official Exa release.

## Plugin

| Plugin | Purpose | Requirements |
| --- | --- | --- |
| `exa` | Searches the web and fetches full pages through Exa. General web research prefers Exa automatically. | Exa account connected through browser OAuth |

## Add This Marketplace to Codex

### Desktop app

1. Open **Codex → Plugins**.
2. Open the Marketplace source menu beside the plugin search field and select **+ Add More**.
3. Paste this repository URL:

   ```text
   https://github.com/zlsbksdxl/codex-exa.git
   ```

4. Select **Codex Exa**, open `exa`, and install it.

Use the Git repository URL, not a raw `marketplace.json` URL. Codex clones the repository and discovers `.agents/plugins/marketplace.json` automatically.

### CLI

```bash
codex plugin marketplace add \
  'https://github.com/zlsbksdxl/codex-exa.git' \
  --ref main \
  --sparse '.agents/plugins' \
  --sparse 'plugins'

codex plugin list --marketplace codex-exa --available --json
codex plugin add exa@codex-exa
```

Fully restart the ChatGPT/Codex desktop app after installation, then use a new task so the Skill and MCP server are reloaded.

## Connect Exa

The plugin uses Exa's official remote MCP OAuth endpoint. During installation, or the first time Exa is used, Codex opens an account connection flow. Sign in to Exa and approve access; no API key is stored in this repository or plugin configuration.

## Update

```bash
codex plugin marketplace upgrade codex-exa
codex plugin add exa@codex-exa
```

## Migrating from the Former Combined Marketplace

The original `codex-plugins` Marketplace was split into this repository and [codex-lark](https://github.com/zlsbksdxl/codex-lark). If the former Marketplace is still configured, remove its installed plugins and source before adding the two new repositories:

```bash
codex plugin remove exa@codex-plugins
codex plugin remove feishu2codex@codex-plugins
codex plugin marketplace remove codex-plugins
```

Then add `codex-exa` using the commands above and add `codex-lark` from its own README.

## Repository Structure

```text
.
├── .agents/plugins/marketplace.json
└── plugins/
    └── exa/
```

## Upstream and Licensing

- [Exa MCP](https://github.com/exa-labs/exa-mcp-server), MIT
- Packaging and documentation in this repository: [MIT](LICENSE)

## Development and Validation

```bash
./scripts/validate-marketplace.sh
```

GitHub Actions runs the same structure check for every push and pull request. Before publishing, also validate the plugin and Skill with Codex's `plugin-creator` and `skill-creator` validators.

See [SECURITY.md](SECURITY.md) for credential and vulnerability reporting guidance.
