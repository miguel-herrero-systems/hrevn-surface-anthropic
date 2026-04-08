# hrevn-baseline-check
Determines profile, readiness, missing blocks, risk flags and next step before a consequential action.
Use this first when you want a pre-flight HREVN assessment.
Example result: `BaselineResult(profile_detected="eu_readiness_profile", readiness_level="medium", ...)`

## When to use
- Before consequential agent actions
- When you need `profile_detected`, `risk_flags`, `missing_required_blocks`
- When a workflow may fall under EU, MiCA or Agentic Finance readiness logic

## When not to use
- Trivial tasks with no consequential action dimension
- Pure conceptual conversations with no structured assessment

## Combination with other HREVN skills
- Use this **first** when more than one HREVN skill is installed
- Pair with `hrevn-sign-on-complete` when you want execution + receipt after the assessment
- Pair with `hrevn-verify-bundle` only after artifacts already exist
- Do **not** call `hrevn-verify-bundle` first if no HREVN artifacts have been generated yet

## Expected output
Return a compact `BaselineResult` with:
- `profile_detected`
- `readiness_level`
- `missing_required_blocks`
- `risk_flags`
- `recommended_next_step`
- `remedy_payload`

## Runtime bridge
When `HREVN_API_KEY` is available, prefer the managed runtime through the local runner:

```bash
python3 scripts/hrevn_anthropic_runner.py baseline-check \
  --input examples/baseline_check_request.json
```

Use `https://api.hrevn.com` as the default backend unless `HREVN_API_BASE_URL`
has been explicitly changed.

If the user asks to run a first test, use:
- `examples/baseline_check_request.json`
- then report the `BaselineResult` returned by the runner
