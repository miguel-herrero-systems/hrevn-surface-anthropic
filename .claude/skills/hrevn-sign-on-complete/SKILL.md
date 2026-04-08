# hrevn-sign-on-complete
Wraps a consequential action so HREVN can run baseline before execution and emit an AER/receipt after execution.
Use this when the action itself needs structured traceability.

## When to use
- When an action should leave a tamper-evident trail
- When you want baseline + action execution + receipt/AER path
- For critical operations in agents and workflows

## When not to use
- Trivial helper functions with no real consequence
- Situations where you only need a pre-flight assessment and no action receipt

## Combination with other HREVN skills
- Recommended order: `hrevn-baseline-check` → `hrevn-sign-on-complete` → `hrevn-verify-bundle`
- If baseline has already been assessed and the action is ready, use this after `hrevn-baseline-check`
- Do not use this instead of `hrevn-baseline-check` when you explicitly need missing blocks / remedy analysis before acting
- `hrevn-verify-bundle` comes after this, not before

## Expected output
A post-action HREVN receipt path:
- baseline artifact
- receipt/AER artifact
- manifest/log path where applicable

## Runtime bridge
Use the managed runtime through the local runner:
1. baseline-check first
2. consequential action second
3. generate-bundle after execution when an artifact is required

Current live backend:
- `https://api.hrevn.com`
