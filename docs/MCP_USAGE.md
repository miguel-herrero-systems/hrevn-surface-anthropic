# HREVN Anthropic MCP Usage

## Goal

Expose the same live HREVN runtime to Claude Code through MCP tools instead of
only through skill guidance plus a local runner.

## Companion server

Use the companion MCP server repo:
- `https://github.com/ai-human-andalusia/hrevn-mcp-server`

It exposes:
- `baseline_check`
- `profile_validate`
- `generate_bundle`
- `verify_bundle`

All four tools call the same managed backend:
- `https://api.hrevn.com`

## Environment

```bash
export HREVN_API_BASE_URL="https://api.hrevn.com"
export HREVN_API_KEY="replace-me"
```

## Install the MCP server

```bash
git clone https://github.com/ai-human-andalusia/hrevn-mcp-server
cd hrevn-mcp-server
pip install -e .
```

If you install into a virtualenv, open Claude Code from that same activated
environment. Otherwise the `hrevn-mcp-server` command may not be available in
the `PATH` Claude Code uses.

## Claude Code config

See:
- `docs/claude_code_mcp_config.example.json`

Put that config in one of:
- `~/.claude/settings.json` for user-level Claude Code config
- `.claude/settings.json` for project-level Claude Code config

Use whichever location your Claude Code installation already reads.

## Verify the MCP server before Claude Code

```bash
cd hrevn-mcp-server
hrevn-mcp-server --version
hrevn-mcp-server --list-tools
hrevn-mcp-server --self-test
```

If the command is not found, run:

```bash
which hrevn-mcp-server
```

and use that absolute path as the MCP `command` value in your Claude Code
configuration.

## Recommended first test

Ask Claude Code to call `baseline_check` with the payload in:
- `examples/baseline_check_request.json`

The expected result is a real `BaselineResult` from the live managed API.

For a real execution record of this path, see:
- `docs/ALPHA_EXECUTION_TRACE.md`

For the concise technical alpha path, see:
- `docs/ANTHROPIC_ALPHA_TESTING.md`
