# How to Rebase the Last Two Commits

This guide explains how to rebase (squash/combine) the last two commits in your Git history.

## Understanding the Current State

The last two commits on the main branch are:
- `3684b2b` - "test"
- `d4b2b1c` - "list" (current HEAD of main)

## Method 1: Interactive Rebase

To squash the last two commits into one:

```bash
# Start an interactive rebase for the last 2 commits
git rebase -i HEAD~2

# In the editor that opens, you'll see something like:
# pick 3684b2b test
# pick d4b2b1c list

# Change the second 'pick' to 'squash' (or 's'):
# pick 3684b2b test
# squash d4b2b1c list

# Save and close the editor
# Another editor will open for you to edit the commit message
# Combine or rewrite the commit messages as desired
# Save and close

# If you've already pushed these commits, you'll need to force push:
# git push --force origin main
```

## Method 2: Soft Reset and Recommit

Alternative approach to combine the last two commits:

```bash
# Soft reset to 2 commits back (keeps changes staged)
git reset --soft HEAD~2

# Now create a new commit with all the changes
git commit -m "Combined commit message"

# If you've already pushed, force push:
# git push --force origin main
```

## Method 3: Using git commit --amend

If you want to merge the last commit into the previous one:

```bash
# Reset the last commit but keep the changes
git reset --soft HEAD~1

# Amend the previous commit with these changes
git commit --amend --no-edit

# Or provide a new message:
# git commit --amend -m "New combined message"

# Force push if needed:
# git push --force origin main
```

## Important Notes

⚠️ **Warning**: Rebasing rewrites Git history. Only do this if:
- You haven't pushed these commits to a shared branch, OR
- You're the only person working on this branch, OR
- You've coordinated with your team and everyone is aware

🔄 **Force Push**: After rebasing, you'll need to force push: `git push --force origin <branch-name>`

## Changes in the Last Two Commits

### Commit 3684b2b "test"
- Created: `hytgfd.txt` (empty file)

### Commit d4b2b1c "list"
- Created: `Nowy dokument tekstowy.txt` with content "1. Lista obecności"
- Deleted: `asd.txt`
- Modified: `test.txt` (removed 1 line)

## Example Combined Commit Message

When squashing these commits, you might use:
```
Add list functionality and test file

- Created new text document for attendance list
- Added test file for validation
- Cleaned up unused files (asd.txt, test.txt)
```
