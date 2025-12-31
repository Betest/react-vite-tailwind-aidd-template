# Agent Protocol

Each iteration:
1) Plan (<=4 bullets)
2) One action (one patch OR one command request)
3) Next check

Rules:
- Do not claim builds/tests pass without logs.
- Minimal diff; no unrelated changes.
- Stop after 3 failed iterations; propose options.
