# Anthropic Alpha Testing

## Public repo

- `https://github.com/miguel-herrero-systems/hrevn-surface-anthropic`

## Companion MCP server

- `https://github.com/miguel-herrero-systems/hrevn-mcp-server`

## Live backend

- `https://api.hrevn.com`

## Supported alpha path

Claude Code -> HREVN MCP server -> `https://api.hrevn.com`

## Quick proof before Claude Code

If you want to verify the runtime path before opening Claude Code, you can use
the installable runner:

```bash
pipx install hrevn-anthropic-runner
export HREVN_API_BASE_URL="https://api.hrevn.com"
export HREVN_API_KEY="replace-with-issued-alpha-key"
hrevn-anthropic health-check
hrevn-anthropic self-test
hrevn-anthropic baseline
```

Expected result:
- a real `BaselineResult`
- returned from the live managed backend

If you want the repo checkout instead, use:

```bash
git clone https://github.com/miguel-herrero-systems/hrevn-surface-anthropic
cd hrevn-surface-anthropic
pipx install .
```

## MCP setup

```bash
git clone https://github.com/miguel-herrero-systems/hrevn-mcp-server
cd hrevn-mcp-server
pip install -e .
```

If you install into a virtualenv, open Claude Code from that same activated
environment so the `hrevn-mcp-server` command is available in the same `PATH`.

## Claude Code config

Use:
- `~/.claude/settings.json` for user-level configuration
- `.claude/settings.json` for project-level configuration

See:
- `docs/claude_code_mcp_config.example.json`

## MCP preflight

Run before opening Claude Code:

```bash
hrevn-mcp-server --version
hrevn-mcp-server --list-tools
hrevn-mcp-server --self-test
```

Expected result:
- the server starts
- four HREVN tools are listed
- the self-test returns a real `BaselineResult`

## First test in Claude Code

Ask Claude Code to call:
- `baseline_check`

with:
- `examples/baseline_check_request.json`

## Important notes

- this is a technical alpha
- the runtime truth is in the managed API
- the MCP server is the supported Anthropic path in this alpha
- the installable runner is the quick proof path, not the main Claude Code path
