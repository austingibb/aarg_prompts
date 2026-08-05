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

Setup, in this order:
1. Run `date +%Y%m%d-%H%M%S` and use its actual output as the timestamp. Do not guess the current date.
2. Ensure a `handoffs/` directory exists at the repo root.
3. Ensure it is ignored locally: if `handoffs/` is not already listed in `.git/info/exclude`, append it. Do not modify the tracked `.gitignore`.
4. List `handoffs/`. If prior handoff files exist, read the two most recent before writing.
5. Run `git status`, `git log --oneline -5`, `git diff --stat`, and `git stash list`. Use the actual output. Do not describe repo state from memory.

Write `handoffs/HANDOFF_<timestamp>.md` containing:
- Previous handoffs: filenames already in this directory, oldest first, or "none".
- Goal: what we are trying to accomplish, and why this approach.
- State: branch, base commit SHA, files modified / staged / untracked, anything stashed. From the commands above.
- Done and verified: complete AND confirmed by a test or manual check. Name the check.
- Done but unverified: written but not yet run. Be strict about this line. If you have not seen it pass, it goes here.
- Remaining: steps left, in the order they should be done.
- Dead ends: approaches tried that failed, and why. Carry forward unresolved entries from prior handoffs. Mark each [carried] or [new].
- Debris: temporary logging, commented-out code, scratch files, hardcoded values that must be removed before shipping. Paths and line numbers. Carry forward anything from prior handoffs, but confirm it is still in the tree first.
- Corrections: any claim in a prior handoff that turned out to be wrong. State the claim and what is actually true. Omit this section if there are none.
- Environment: exact build / run / test commands, plus services, env vars, or ports required.
- Gotchas: anything surprising about this codebase that cost you time.

This file must stand alone for current state. The next agent should not need to read older handoffs to continue.

Finally, output in a single fenced code block a short prompt I can paste into the next agent. It must name the exact filename you just wrote, tell the agent to read it, verify the described state against the actual repo before trusting it, and continue from the first item under Remaining. Use the real filename, not a placeholder.

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
