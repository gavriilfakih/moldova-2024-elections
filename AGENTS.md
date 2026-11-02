# Moldova 2024 elections

- Search for prior art before building anything new: existing tools, libraries and CLIs, GitHub included (`gh search repos`, `gh search code`, `gh repo view`). Report what exists and why it is not being adopted.
- Clone a third-party repository and read it locally rather than browsing it through the GitHub API.
- Use `uv` for Python environments and tools; never use `pip`, `pip3` or `pipx`.
- Use `pnpm` for Node and JavaScript projects; do not substitute `npm` or `yarn`.
- Use `zsh` for shell-specific work and prefer POSIX-compatible commands where practical.
- Do not add dependencies without flagging the addition.
- Check current documentation before coding against a niche tool or API.
- Tasks live in `~/Vault/Projects/moldova-2024-elections/TODO.md`, which replaces the usual root `TODO.md`. Read it before starting work, set a task `[/]` when you start it and `[X]` when it is done, and add tasks you find but do not do.

## Git

This repository is public. Anything pushed to `origin`, on any branch, is published and cannot be reliably withdrawn.

- `main` holds only finished, checked work, one squashed commit per change. The owner merges locally with `git merge --squash`, without pull requests; an agent merges only when the owner asks in that session.
- Work happens on a branch named for whoever is doing it: `dev/<topic>` for the owner, `claude/<topic>` for Claude, `codex/<topic>` for Codex. An agent works only on its own prefix.
- The main checkout is the owner’s; an agent leaves its branch alone. Before its first edit, an agent creates a worktree from `main` and links the data from inside it:
  - Claude: `git worktree add .claude/worktrees/<topic> -b claude/<topic> main`, then enter it by path.
  - Codex: `git worktree add .worktrees/<topic> -b codex/<topic> main`.
  - Data: `ln -s "$(git rev-parse --path-format=absolute --git-common-dir)/../data" data`.
- An agent commits only when the owner asks, and only on its own branch. It pushes or creates a remote only when the owner asks in that session.
- Delete a branch once it is merged. Tag what was presented or submitted, e.g. `csdc-2026-11-04`.
- Keep large generated files, data, images and binaries out of Git; update `.gitignore` proactively.

## The project

Research on pro-Russian Telegram and the Moldovan press around Moldova’s 2024 presidential election and EU referendum, for talks, conference papers and a journal article. Background and working notes: `~/Vault/Projects/moldova-2024-elections/`.

## Citation

Cite sources by their Zotero citation keys using pandoc.

## Data

`data/` is ignored by git and supplied by each machine, as a folder or a link. It holds the raw corpora and the earlier processed outputs, which are the baseline the re-run is compared against: treat both as read-only. `data/raw/telegram-extended/` is about 90 GB of archived media: don’t read it in bulk or trigger a download.

- `code/` is tracked, `paper/` stays empty on `main` for now, and `output/` is ignored. `annotation/` tracks only the codebook, because coded samples contain message texts.
- Never commit message or article texts, anything else from `data/`, or anything derived that reproduces them.
- Commit a notebook only with its outputs stripped, after checking it for API credentials.
