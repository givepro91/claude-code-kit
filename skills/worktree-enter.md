Create a new git worktree for the current task and switch into it within this Claude Code session.

## Usage
```
/worktree-enter [task-name]
```
Examples: `/worktree-enter scheduler`, `/worktree-enter` (auto-generated name)

## Steps

1. Extract the task name from the argument.
   - If provided, use that name.
   - If omitted, generate one from the current date: `task-MMDD-{random 4 hex}`
     Example: `task-0316-a3f2`

2. Call the `EnterWorktree` tool with the task name as the `name` parameter.

3. After entry, show this summary:
```
Worktree entered

Branch: <branch-name>
Path:   <worktree-path>

To leave:
  /worktree-exit keep    # preserve branch
  /worktree-exit remove  # delete worktree
```

## Notes

- Cannot nest — if already in a worktree, refuse entry. Check with `git worktree list` and compare the current directory against the list.
- This switches the current session's working directory, no new terminal needed.
- Consider merging with `--no-ff` to preserve branch history in the git log.
