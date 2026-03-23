# The `.claude/` Directory Guide

Claude Code uses a `.claude/` directory in your project root for configuration.

## Structure

```
.claude/
├── commands/          # Custom slash commands (skills)
│   ├── worktree-enter.md
│   └── my-skill.md
├── rules/             # Contextual rules loaded automatically
│   └── security.md
└── settings.json      # Project-level permissions and config
```

## commands/

Each `.md` file becomes a `/slash-command` in Claude Code.

- Filename = command name: `worktree-enter.md` → `/worktree-enter`
- Content = prompt that Claude executes when you invoke the command
- Can accept arguments: `/worktree-enter my-task` passes `my-task` as input

### Writing a good skill

1. **First line**: One-sentence description of what it does
2. **Steps section**: Numbered instructions Claude follows
3. **Notes section**: Edge cases, constraints, tips

Example:
```markdown
Run the test suite and report failures with suggested fixes.

## Steps

1. Run `npm test` and capture output.
2. If all tests pass, report success.
3. If tests fail, analyze each failure and suggest a fix.

## Notes

- Skip snapshot update suggestions unless the user asks
```

## rules/

Rules are automatically loaded into Claude's context based on file patterns.

```markdown
---
paths: ["src/api/**", "scripts/*.sh"]
---

## API Rules

- All endpoints must validate input with zod
- Scripts must start with set -euo pipefail
```

- `paths:` frontmatter controls when the rule activates
- Without `paths:`, the rule loads for every conversation
- Great for: security policies, coding standards, project conventions

## settings.json

Controls permissions and tool access at the project level.

```json
{
  "permissions": {
    "allow": ["Read", "Write", "Bash(npm run *)"],
    "deny": ["Bash(rm -rf *)"]
  }
}
```

## Tips

- Commit `.claude/commands/` and `.claude/rules/` to share with your team
- Keep `settings.json` project-specific (don't put secrets in it)
- Skills can reference other skills: "Run `/code-review` on the changed files"
