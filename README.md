# git-worktrees

Interactive script to quickly navigate to git worktrees. Scans `~/` (max depth 3) for git repos that have worktrees, lets you pick a repo, then a worktree, and `cd` there.

Works with **bash** and **zsh**.

## Dependencies

### Required (POSIX / standard Unix)
- **git** — must support `git worktree list` (Git 2.5+)
- **find**, **awk**, **sort**, **cut** — standard Unix tools

### Optional (recommended)
- **[fzf](https://github.com/junegunn/fzf)** — fuzzy finder for interactive selection. Without it, the script falls back to a numbered menu.

## Setup

### 1. Clone the repo
```bash
git clone <this-repo> ~/dev/worktrees-bash
```

### 2. Make the script executable
```bash
chmod +x ~/dev/worktrees-bash/git-worktrees
```

### 3. Add to your shell config

You must **source** the script (not run it) so it can change your shell’s current directory.

**Bash** (add to `~/.bashrc` or `~/.bash_profile`):
```bash
alias wt='source ~/dev/worktrees-bash/git-worktrees'
```

**Zsh** (add to `~/.zshrc`):
```bash
alias wt='source ~/dev/worktrees-bash/git-worktrees'
```

Reload your config: `source ~/.zshrc` or `source ~/.bashrc`.

### 4. Install fzf (optional, recommended)
```bash
# macOS (Homebrew)
brew install fzf

# Linux
# See https://github.com/junegunn/fzf#installation
```

With fzf you get fuzzy search; without it, a numbered menu is used.

---

## Usage

Run with no arguments:

```bash
wt
```

### Flow

1. **Pick a repo** — Lists git repos under `~/` (depth ≤ 3) that have worktrees.
2. **Pick a worktree** — Shows main worktree, branch-backed worktrees, and detached HEADs.
3. Your shell `cd`s into the chosen directory.

### With fzf

- Fuzzy-search repo names and paths at both prompts.
- Type to filter; Enter selects; Esc or Ctrl+C exits without changing directory.

### Without fzf

- Numbered menus printed to stderr.
- Enter the number and press Return.

### Single repo/worktree

- If only one repo exists, it is chosen automatically.
- If only one worktree exists for that repo, you jump straight there.

### Notes

- Arguments are not supported; run with no args.
- Worktrees are ordered: main first, then branch-backed, then detached.
