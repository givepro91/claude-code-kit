# claude-code-kit

Ready-to-use skills and workflows for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

![demo](demo.gif)

## What's included

| Skill | Description |
|-------|-------------|
| `/worktree-enter` | Create an isolated git worktree and switch into it — no new terminal needed |
| `/worktree-exit` | Leave the worktree and return to your default branch — keep or remove |
| `/code-review` | Structured code review for simplicity, clarity, correctness, and security |

## Quick install

Clone the repo and run the installer in your project:

```bash
git clone https://github.com/givepro91/claude-code-kit.git
cd your-project
bash /path/to/claude-code-kit/install.sh
```

Or install directly (review the [script](install.sh) first):

```bash
curl -fsSL https://raw.githubusercontent.com/givepro91/claude-code-kit/main/install.sh | bash
```

The installer will:

1. Let you pick which skills to install
2. Copy selected skills to `.claude/commands/`
3. Generate `scripts/setup-worktree.sh` with your custom symlink targets (if worktree skills selected)
4. Optionally update `.gitignore`

**After install:** restart Claude Code or start a new session — then type `/worktree-enter` to verify.

## Skills

### `/worktree-enter [task-name]`

Creates an isolated git worktree for your task and switches Claude Code's working directory into it.

```
You: /worktree-enter auth-refactor

Claude: Worktree entered
        Branch: feat/auth-refactor
        Path:   ../worktrees/auth-refactor
```

- Auto-generates a name if omitted (`task-0323-a3f2`)
- Runs `setup-worktree.sh` to symlink shared files you configured during install
- No nested entry — checks if you're already in a worktree

### `/worktree-exit [keep|remove]`

Leaves the worktree and returns to the main repo.

- `keep` — preserve the branch for later (re-enter with `/worktree-enter`)
- `remove` — delete the worktree and branch
- No argument — prompts you to choose

### `/code-review [file-or-path]`

Analyzes code on four axes:

- **Simplicity** — can anything be removed or simplified?
- **Clarity** — is the intent obvious? Are names descriptive?
- **Correctness** — bugs, edge cases, off-by-one errors?
- **Security** — injection, credential exposure, common vulnerabilities?

If no file is given, reviews staged or unstaged git changes.

## Merge tip

Consider merging worktree branches with `--no-ff` to preserve branch history:

```bash
git merge --no-ff <branch-name> -m "merge: <branch-name>"
```

## Project structure

```
claude-code-kit/
├── install.sh              # Interactive installer
├── skills/
│   ├── worktree-enter.md   # /worktree-enter skill
│   ├── worktree-exit.md    # /worktree-exit skill
│   └── code-review.md      # /code-review skill
├── scripts/
│   └── setup-worktree.sh   # Worktree symlink setup (template)
└── docs/
    └── claude-directory-guide.md  # How .claude/ directory works
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- Git 2.15+ (worktree support)

## Learn more

- [`.claude/` directory guide](docs/claude-directory-guide.md) — how commands, rules, and settings work

## License

MIT
