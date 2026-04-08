# hrevn-verify-bundle
Inspects HREVN baseline, receipt, manifest and related artifacts and explains what happened.
Use this when artifacts already exist and you want verification or interpretation.

## When to use
- When HREVN artifacts already exist
- When you want to inspect baseline, receipt, manifest or JSONL logs
- When you need to explain what happened in a prior HREVN-protected run

## When not to use
- Before any HREVN artifacts have been generated
- As a replacement for `hrevn-baseline-check` on a fresh workflow

## Combination with other HREVN skills
- Usually this is the **third** skill in the chain
- Recommended order: `hrevn-baseline-check` → `hrevn-sign-on-complete` → `hrevn-verify-bundle`
- If only inspection is needed and artifacts already exist, this can be used alone
- Do not use this first for a new workflow with no receipt/bundle yet

## Expected output
A concise verification summary of:
- run id
- profile
- readiness
- success/failure
- artifact set present/missing
- what is verified vs merely described

## Runtime bridge
When a bundle zip exists, prefer:

```bash
python3 scripts/hrevn_anthropic_runner.py verify-bundle \
  --source /absolute/path/to/bundle.zip
```

Use the managed verifier result to separate verified integrity from descriptive
summary.
