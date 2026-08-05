```
Summarize your findings in a single prompt I will pass to a coding agent.
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
