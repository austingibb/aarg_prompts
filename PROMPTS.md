```
Write a single self-contained prompt that I will paste into a fresh coding agent. Output only that prompt, in one fenced code block, with no commentary around it.

The receiving agent has the repo but none of this conversation. Assume it knows nothing you have not written down. Address it directly, in the imperative.

Include, in this order:
1. Task: what needs to be done, in one or two sentences.
2. Verified findings: each with a `path/to/file.ext:line` pointer and the relevant symbol name. Label anything you inferred but did not confirm as UNVERIFIED.
3. Ruled out: hypotheses you eliminated and the evidence that eliminated them.
4. Open questions: what the next agent must still resolve, with a suggested way to resolve each.
5. Constraints: files or systems not to touch, conventions to follow, existing patterns to mirror (cite an example location).
6. Done criteria: the command, test, or observable behavior that shows the task is complete.

Rules:
- File paths and facts over narrative. No recap of your investigation process.
- Never reference this conversation, "above", "as we discussed", or anything outside the repo.
- Tool-agnostic: no slash commands, no agent-specific config files or features.
- Under 400 words. Cut background before cutting file references.
```

```
Hand this work off to a different coding agent (OpenCode, Claude Code, Codex, or similar).

First, run `git status`, `git log --oneline -5`, `git diff --stat`, and `git stash list`. Use the actual output. Do not describe repo state from memory.

Then write `HANDOFF.md` at the repo root containing:
- Goal: what we are trying to accomplish, and why this approach.
- State: branch, base commit SHA, which files are modified / staged / untracked, anything stashed. Taken from the commands above.
- Done and verified: complete AND confirmed by a test or manual check. Name the check.
- Done but unverified: written but not yet run. Be strict about this line. If you have not seen it pass, it goes here.
- Remaining: the steps left, in the order they should be done.
- Dead ends: approaches tried that failed, and why, so they are not retried.
- Debris: temporary logging, commented-out code, scratch files, hardcoded values you introduced that must be removed before this ships. Give paths and line numbers.
- Environment: exact build / run / test commands, plus services, env vars, or ports required.
- Gotchas: anything surprising about this codebase that cost you time.

Finally, output in a single fenced code block a short prompt I can paste into the next agent, telling it to read `HANDOFF.md`, verify the described state against the actual repo before trusting it, and continue from the first item under Remaining.

Be accurate rather than flattering about your own progress. Work described as finished that is not finished is the most expensive error here.
```

```
Summarize everything discussed and decided and done in this chat so I can recall the important things we worked on/discussed.
```

```
Commit all current work as a single commit.

1. Review first: run `git status` and `git diff` before staging. Stage everything including untracked files, but exclude build artifacts, local config, secrets, and anything that should be gitignored (add it to .gitignore if it isn't there).
2. Message format:
   - Subject: one line, imperative mood, 72 chars or fewer, no trailing period.
   - Blank line.
   - Body: two or three paragraphs covering what changed, why it changed, and any tradeoffs or known follow-up work. Wrap at 72 chars.
3. No AI attribution anywhere in the commit: no Co-Authored-By trailers, no "Generated with" footers, no tool names, no emoji.
4. Do not push, amend, or rebase. Stop after the commit.
```
