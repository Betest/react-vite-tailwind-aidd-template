# AI Rules (Repository)

## Hard rules
- Do NOT invent file contents, command output, test results, or tool responses.
- If needed, ask to read/search/run via available tooling.
- Make minimal, scoped edits. No drive-by refactors.
- Keep behavior unchanged unless explicitly requested.

## Iteration protocol
Each iteration must follow:
1. Plan (max 4 bullets)
2. One action (one patch OR one tool request)
3. Next check (what to run / what output is needed)

## Loop limit
After 3 failed iterations, STOP:
- Summarize evidence (errors, failing tests, logs).
- Provide 2–3 options to proceed.
- Ask the user to choose.

## Token efficiency
- Be concise. Bullets over paragraphs.
- No repeated context or long explanations unless asked.
- Prefer diffs over full files.

## Patch conventions
- Avoid formatting-only changes.
- Prefer small diffs, one concern per commit.
- Add/adjust tests when changing logic or migrating APIs.
