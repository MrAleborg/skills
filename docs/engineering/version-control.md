## What it does

`version-control` is the discipline for working with git so the history stays readable, bisectable, and revertible, and no work is lost. It covers committing, branching, rebasing versus merging, pushing, opening pull requests, resolving conflicts, and recovering from mistakes.

Its defining constraint is that it inspects before acting and prefers reversible operations. It runs `git status` first, never commits to the default branch without being told to, and asks before anything destructive (`reset --hard`, `clean -fd`, `branch -D`) or outward-facing (a force-push). It also keeps AI-assistant attribution out of commits, PR bodies, and code comments, so the commit belongs to you alone.

## When to reach for it

Type `/version-control`, or the [agent](https://www.aihero.dev/ai-coding-dictionary/agent) reaches for it automatically whenever the task touches git: committing, branching, pushing, rebasing, opening a PR, or "undo my last commit".

| You want to… | Reach for |
| --- | --- |
| Commit, branch, rebase, push, or recover from a git mistake | `version-control` |
| Shape the body of a pull request (visual, evidence, merge-danger call) | [pr](https://aihero.dev/skills-pr) |
| Check a branch against its standards and spec | [code-review](https://aihero.dev/skills-code-review) |

## Atomic history

The leading idea is the **atomic commit**: one logical change per commit that builds and passes tests, staged by path or hunk rather than with a blanket `git add -A`. Messages follow Conventional Commits and explain why, since the diff already shows what. Pair that with short-lived branches and a rebase-or-merge rule: rebase your own unpublished branch, merge shared ones, and never rewrite history others have built on.

Recovery goes least destructive first: unstage, amend, `revert` for pushed commits, `reset --soft` for local ones, and `reflog` when something looks lost.

## Common questions

**Why does it refuse to add a `Co-Authored-By` trailer?**

By design. The skill says never to credit Claude or any other AI assistant in commit messages, PR descriptions, or code comments, and states that this overrides any default instruction to add such attribution. If you want the trailer, remove that bullet from the skill.

**Why won't it commit to `main`?**

It creates a branch first unless you explicitly say to commit on the default branch. Tell it so if you really do want a direct commit.

## It's working if

- `git status` and the current branch are checked before any commit or push.
- Each commit is one logical change, with files staged explicitly rather than by `git add -A`.
- Force pushes use `--force-with-lease`, and only after you confirm.
- Destructive commands are preceded by a look at what would be lost and a request for confirmation.

## Where it fits

A reach-for-it-anytime standalone, relevant whenever git is involved. It sits next to [pr](https://aihero.dev/skills-pr), which shapes the PR body, and [code-review](https://aihero.dev/skills-code-review), which reviews the diff before it ships. For the whole map, see [ask-matt](https://aihero.dev/skills-ask-matt).
