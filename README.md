# claude-code-kit

Ready-to-use skills and workflows for [Claude Code](https://docs.anthropic.com/en/docs/claude-code).

## What's included

| Skill | Description |
|-------|-------------|
| `/worktree-enter` | Create an isolated git worktree and switch into it — no new terminal needed |
| `/worktree-exit` | Leave the worktree and return to main — keep or remove the branch |
| `/code-review` | Quick code review using Rob Pike's simplicity principles |

## Quick install

```bash
# In your project root
curl -fsSL https://raw.githubusercontent.com/givepro91/claude-code-kit/main/install.sh | bash
```

Or clone and run locally:

```bash
git clone https://github.com/givepro91/claude-code-kit.git
cd your-project
bash /path/to/claude-code-kit/install.sh
```

The installer will:

1. Create `.claude/commands/` with selected skills
2. Generate `scripts/setup-worktree.sh` with your custom symlink targets
3. Optionally update `.gitignore`

## Skills

### `/worktree-enter [task-name]`

Creates an isolated git worktree for your task and switches Claude Code's working directory into it.

```
You: /worktree-enter auth-refactor

Claude: Worktree 진입 완료
        Branch: feat/auth-refactor
        Path:   ../swk-worktrees/auth-refactor
```

- Auto-generates a name if omitted (`task-0323-a3f2`)
- Runs `setup-worktree.sh` to symlink shared files (`.env`, config, etc.)
- No nested entry — checks if you're already in a worktree

### `/worktree-exit [keep|remove]`

Leaves the worktree and returns to the main repo.

- `keep` — preserve the branch for later (re-enter with `/worktree-enter`)
- `remove` — delete the worktree and branch
- No argument — prompts you to choose

### `/code-review`

Analyzes selected code for simplicity, clarity, and potential issues.

## Merge rule

Always merge worktree branches with `--no-ff` to preserve branch history:

```bash
git merge --no-ff feat/my-task -m "merge: feat/my-task → main"
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
    └── claude-directory-guide.md
```

## Requirements

- [Claude Code](https://docs.anthropic.com/en/docs/claude-code) CLI
- Git 2.15+ (worktree support)

## License

MIT
