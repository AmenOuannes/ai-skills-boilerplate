# Cherry-pick a commit into another branch

## What it does
Takes a commit from one branch and applies it cleanly to another branch, using git cherry-pick and optionally creating or updating a PR.

## When to use it
Use this skill when a fix or feature on one branch needs to be backported, hotfixed, or applied to a different line of development.

## Inputs
- Source commit SHA or range
- Target branch name
- Optional: whether to open a PR after cherry-picking
- Optional: conflict resolution preferences

## Output
- Cherry-picked commit on the target branch
- Optional PR link
- A summary of what was applied and any conflicts resolved

## Steps

1. **Identify the source commit**
   - Confirm the commit SHA, subject, and original branch.
   ```bash
   git log --oneline <source-branch> -n 10
   ```

2. **Fetch and checkout the target branch**
   ```bash
   git fetch origin
   git checkout -b <target-branch>-cherry-pick-<sha-short> origin/<target-branch>
   ```

3. **Cherry-pick the commit**
   ```bash
   git cherry-pick <commit-sha>
   ```

4. **Handle conflicts if they occur**
   - List conflicted files:
     ```bash
     git status --short
     ```
   - Resolve each conflict manually.
   - Stage resolved files:
     ```bash
     git add <file>
     ```
   - Continue the cherry-pick:
     ```bash
     git cherry-pick --continue
     ```

5. **Run checks**
   - Run tests, lint, and type checks for the target branch.

6. **Push and optionally open a PR**
   ```bash
   git push -u origin <target-branch>-cherry-pick-<sha-short>
   ```

   If a PR is needed:
   ```bash
   gh pr create \
     --base <target-branch> \
     --title "cherry-pick: <original-subject>" \
     --body "Cherry-picks <commit-sha> from <source-branch> into <target-branch>."
   ```

7. **Confirm**
   - Print the new commit SHA, branch name, and PR link if created.

## Rules
- Prefer cherry-picking individual commits over ranges when possible.
- If cherry-picking a merge commit, use `-m 1` and explain why.
- Do not force-push to shared target branches.
- If conflicts are too large or risky, stop and ask the user before resolving.
- Mention the original commit SHA in the new commit message or PR body for traceability.
