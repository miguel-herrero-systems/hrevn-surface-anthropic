# Anthropic Alpha Execution Trace

This document records a real technical alpha execution against the live HREVN
managed runtime through the HREVN MCP server.

## Public repos

- `https://github.com/miguel-herrero-systems/hrevn-surface-anthropic`
- `https://github.com/miguel-herrero-systems/hrevn-mcp-server`

## Live backend

- `https://api.hrevn.com`

## MCP server checks

Version:

```bash
PYTHONPATH=/Users/miguelmiguel/Documents/Playground/HREVN_REORG/hrevn-mcp-server/src \
python3 -m hrevn_mcp_server.server --version
```

Real output:

```text
0.1.0-alpha
```

Registered tools:

```bash
PYTHONPATH=/Users/miguelmiguel/Documents/Playground/HREVN_REORG/hrevn-mcp-server/src \
python3 -m hrevn_mcp_server.server --list-tools
```

Real output:

```text
baseline_check
profile_validate
generate_bundle
verify_bundle
```

## Live self-test

Command:

```bash
HREVN_API_BASE_URL=https://api.hrevn.com \
HREVN_API_KEY=<issued-alpha-key> \
PYTHONPATH=/Users/miguelmiguel/Documents/Playground/HREVN_REORG/hrevn-mcp-server/src \
python3 -m hrevn_mcp_server.server --self-test
```

Real output:

```json
{
  "content": [
    {
      "type": "text",
      "text": "{'output_version': '1.0', 'result': 'BASELINE_CHECK_COMPLETE', 'profile_detected': 'eu_readiness_profile', 'readiness_level': 'medium', 'missing_required_blocks': ['human_oversight', 'risk_register', 'evidence_lifecycle', 'technical_documentation_refs'], 'risk_flags': ['missing_human_oversight', 'missing_risk_register', 'missing_evidence_lifecycle', 'missing_technical_documentation_refs'], 'recommended_next_step': 'collect_missing_fields', 'remedy_payload': {'human_oversight': {'reviewer': None, 'approval_reference': None}, 'risk_register': {'risk_id': None, 'mitigation': None}, 'evidence_lifecycle': {'retention_policy': None, 'evidence_reference': None}, 'technical_documentation_refs': {'system_description_ref': None, 'limitations_ref': None, 'human_oversight_procedure_ref': None, 'logging_policy_ref': None}}, 'check_id': 'CHK-AF454ADA7044', 'checked_at': '2026-04-08T20:06:02+00:00'}"
    }
  ],
  "isError": false,
  "structuredContent": {
    "output_version": "1.0",
    "result": "BASELINE_CHECK_COMPLETE",
    "profile_detected": "eu_readiness_profile",
    "readiness_level": "medium",
    "missing_required_blocks": [
      "human_oversight",
      "risk_register",
      "evidence_lifecycle",
      "technical_documentation_refs"
    ],
    "risk_flags": [
      "missing_human_oversight",
      "missing_risk_register",
      "missing_evidence_lifecycle",
      "missing_technical_documentation_refs"
    ],
    "recommended_next_step": "collect_missing_fields",
    "remedy_payload": {
      "human_oversight": {
        "reviewer": null,
        "approval_reference": null
      },
      "risk_register": {
        "risk_id": null,
        "mitigation": null
      },
      "evidence_lifecycle": {
        "retention_policy": null,
        "evidence_reference": null
      },
      "technical_documentation_refs": {
        "system_description_ref": null,
        "limitations_ref": null,
        "human_oversight_procedure_ref": null,
        "logging_policy_ref": null
      }
    },
    "check_id": "CHK-AF454ADA7044",
    "checked_at": "2026-04-08T20:06:02+00:00"
  }
}
```

What this validates:
- the MCP server starts correctly
- the tool registry is visible
- the MCP server reaches the live managed backend
- the backend returns a real `BaselineResult`

## Summary

This confirms the Anthropic technical alpha path works as intended:

- Claude Code or MCP-compatible client
- HREVN MCP server
- live runtime behind `https://api.hrevn.com`
