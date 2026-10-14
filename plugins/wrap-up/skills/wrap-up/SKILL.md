---
name: wrap-up
description: End-of-session wrap-up. Save any new durable knowledge from this session to memory, commit the session's code changes in clean, scoped commits, then start the next session on a handoff prompt and switch to it. Use when the user wants to wrap up, finish, close out, or commit a session's work along with what was learned.
argument-hint: "[optional note — scope hint or commit theme] [-n|--no-handoff to skip Phase 3]"
---

# Wrap Up

$ARGUMENTS

Two-phase close-out for the current session. Memory first, then commits — in that order, because writing memories often clarifies what the commits should say.

## Phase 1 — Memory

Review this session's conversation and decide what (if anything) is worth persisting to `/Users/cole/.claude/projects/-Users-cole/memory/`. Follow the rules in the user's global instructions for memory (`user` / `feedback` / `project` / `reference` types; never save code patterns, file paths, or git-derivable facts).

Be selective. Most sessions produce zero memories. Good candidates:

- **Feedback**: a correction or validated approach you'd want to honor next time ("don't mock the DB", "yes, one bundled PR was right")
- **Project**: a decision, deadline, or motivation that isn't in the code or commit messages
- **User**: a new fact about the user's role, expertise, or preferences
- **Reference**: a pointer to an external system (Linear project, Grafana board, Slack channel)

For each memory:
1. Write the memory file with proper frontmatter (`name`, `description`, `type`).
2. Add a one-line index entry to `MEMORY.md`.
3. If updating an existing memory, edit in place rather than creating a duplicate.

If nothing is worth saving, say so in one line and move on.

**Show the user the list of memories you wrote/updated before moving to Phase 2.**

## Phase 2 — Commits

Now commit the session's code work.

1. **Survey state** — run `git status` and `git diff` (staged + unstaged) in parallel. If not in a git repo, stop and tell the user.
2. **Check log style** — `git log -10 --oneline` to match this repo's commit message conventions.
3. **Group changes into scoped commits.** Don't dump everything into one commit unless it really is one logical change. Split by concern: feature vs. refactor vs. fix vs. docs. Memory file changes (under `~/.claude/`) are *not* part of the project repo — never stage them into a project commit.
4. **Draft messages** that explain *why*, not *what*. Follow the repo's existing style (subject length, conventional-commits prefix or not, etc.).
5. **Stage explicitly** — `git add <files>`, never `git add -A` or `git add .`. Skip anything that looks like a secret.
6. **Commit** with a HEREDOC for the message. Do not skip hooks. Do not amend.
7. If a hook fails, fix the underlying issue and make a **new** commit — never `--amend`.
8. Run `git status` after each commit to verify.

**Push sensible finished work to Cole's own repos without asking.** Ask before force-pushing, rewriting history, or pushing to shared or work repos.

## Phase 3 — Hand off to a fresh session

**Skip this phase entirely if `$ARGUMENTS` contains `-n` or `--no-handoff`.** Note it in the output summary ("handoff skipped per flag") and stop.

Write the prompt that lets a **fresh native agent session** pick up where this one ended, then start that session yourself — the user should not have to paste anything.

Write it as if **the user is speaking to a new agent**, first person ("I was working on..."), not as a third-party report. It should be self-contained — the new session won't have any of this conversation's context, and loads its provider’s project instructions. Include relevant memory pointers rather than assuming both providers load the same memory files.

Include only what's load-bearing for resuming:

- **What I was doing** — one or two sentences naming the project and the goal.
- **Where things stand** — branch name, what just got committed (reference SHAs or subjects from Phase 2), what's still uncommitted or WIP.
- **What's next** — the specific next step or open question. If there are decisions pending, name them.
- **Gotchas** — anything non-obvious the next session would otherwise stumble on (a flaky test, a half-applied refactor, a config quirk). Skip if none.
- **Pointers** — file paths, PR/issue numbers, or memory filenames worth reading first. Use `file:line` where useful.

Keep it **tight** — aim for under ~200 words. A new session reading a wall of text is no better than starting blind.

Then hand over, in this order:

1. **Print the output summary first.** The handoff ends this session a couple of seconds later, so anything printed after it is never seen.
2. Write the prompt — raw text, no fence, no surrounding prose — to a file under `${TMPDIR:-/tmp}`.
3. Run `~/dotfiles/zsh/common/agent-handoff <that file>`.

`agent-handoff` inherits the current provider (`AGENT_PROVIDER`, default Codex), accepts `--provider codex|claude`, and forces work Claude under `~/Work`. It starts a fresh native conversation in this directory with the briefing. Once the replacement's prompt hook confirms startup, it moves clients viewing the source pane and retires only that pane. Siblings survive.

On timeout or startup failure, the source remains open. Report the failure and any replacement pane printed by the helper; do not blindly retry and create duplicates. A trust or login prompt may need the user in that replacement. Outside tmux, print the briefing in a fenced `text` block and copy it with `pbcopy` instead. After a successful handoff, do not run further commands.

If the session genuinely has no continuation (one-off task, fully closed out), say so in one line and skip the handoff entirely.

## Output

End with a tight summary:
- Memories written/updated (filenames only)
- Commits created (short SHA + subject line)
- Handoff — the new session it starts, or "no handoff needed"
- Anything skipped and why (e.g. "left WIP changes in `foo.ts` unstaged — incomplete")
