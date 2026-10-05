# eval/

Model evaluation harness. Only for products that call an LLM at runtime; delete the folder otherwise.

## Files
- `cases.jsonl` — one test case per line: `{"id": "...", "input": ..., "expected": ..., "tags": ["nominal" | "edge" | "injection"]}`
- `models.yaml` — candidates to compare (provider, model id, pinned revision, hosting). Same config format as the product's provider layer, so the product and the eval call models the same way.
- runner — `npm run eval` (Node) or `python -m eval` (Python); writes `eval/results/latest.json` and prints a markdown table for `docs/MODEL_EVAL.md`.

## Runner contract
1. Load `models.yaml`; skip a hosted candidate whose API key env var is missing, and say so.
2. For each case × model: call through the product's provider abstraction, record output, latency, tokens.
3. Score with a deterministic scorer (exact match, schema validation, rule-based rubric).
4. Exit non-zero if the chosen model's quality is below `EVAL_MIN_QUALITY` (from the model-selection ADR).

No real personal data in `cases.jsonl`. Results are committed only as the summary table in `docs/MODEL_EVAL.md`.
