Leave the worktree created by `/worktree-enter` and return to the main repository.

## Usage
```
/worktree-exit [keep|remove]
```
Examples: `/worktree-exit keep`, `/worktree-exit remove`, `/worktree-exit` (prompts)

## Steps

1. Check the argument.
   - `keep` — preserve the branch and worktree directory, return to main
   - `remove` — delete the worktree, return to main
   - No argument — prompt the user:
     ```
     How do you want to exit?
     1. keep   — preserve branch (resume later)
     2. remove — delete worktree (done or discarding)
     ```

2. Call the `ExitWorktree` tool with the chosen action.
   - If `remove` is chosen and there are uncommitted changes, the tool will refuse.
     Ask the user to confirm, then retry with `discard_changes: true`.

3. After returning, show a summary:
   - If `keep`:
     ```
     Worktree preserved

     Branch <branch-name> is kept.
     Re-enter later: /worktree-enter <task-name>

     To merge into main:
       git merge --no-ff <branch-name> -m "merge: <branch-name> → main"
     ```
   - If `remove`:
     ```
     Worktree removed. Back on main.
     ```

## Notes

- Only works for worktrees created via `/worktree-enter`
- On session end, a keep/remove prompt appears automatically
