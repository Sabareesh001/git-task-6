# Task 6: Git Stash - Temporarily Saving Work

## Objective

Learn how to use git stash to save work in progress without committing:

- Stash changes temporarily
- Apply stashed changes later
- Manage multiple stashes
- Use stash in various workflows
- Understand when to use stash vs. commit

## Setup Instructions

This task is part of the git-fundamentals project. Ensure you have:

- Git installed on your system
- A local git repository initialized in this directory
- Understanding of git commits and working directory
- Familiarity with tracked and untracked files
- A code editor (VS Code recommended)

## Exercise Overview

Git stash is a helpful tool for temporarily saving changes in your working directory without committing them. This is useful when you need to switch branches or work on something else before finishing your current task.

### 1. Basic Stashing - Saving Work

**Command:**

```bash
git stash
```

or with a description:

```bash
git stash save "Work in progress on feature X"
```

or with modern Git (2.13+):

```bash
git stash push -m "Work in progress on feature X"
```

This command:
- Saves all tracked file changes in the working directory
- Reverts working directory to the last committed state
- Does NOT stash untracked files by default

**Example:**

```bash
# You have modified files but haven't committed
git status
# On branch feature-branch
# Changes not staged for commit:
#   modified: index.html
#   modified: styles.css

git stash
# Saved working directory and index state WIP on feature-branch
```

### 2. Stashing Untracked Files

To include untracked files in your stash:

```bash
git stash -u
```

or

```bash
git stash --include-untracked
```

To stash only untracked files:

```bash
git stash -o
```

### 3. Viewing Stashed Changes

**List all stashes:**

```bash
git stash list
```

**Output example:**

```
stash@{0}: WIP on feature-branch: Work in progress on feature X
stash@{1}: WIP on main: Fixed bug in login
stash@{2}: On develop: Updated documentation
```

**View details of a specific stash:**

```bash
git stash show stash@{0}
```

**View the actual changes in a stash:**

```bash
git stash show -p stash@{0}
```

### 4. Applying Stashed Changes

**Apply the most recent stash (keeps it in the list):**

```bash
git stash apply
```

**Apply a specific stash:**

```bash
git stash apply stash@{2}
```

**Apply and remove the stash (pop):**

```bash
git stash pop
```

**Apply and remove a specific stash:**

```bash
git stash pop stash@{1}
```

### 5. Deleting Stashes

**Delete the most recent stash:**

```bash
git stash drop
```

**Delete a specific stash:**

```bash
git stash drop stash@{2}
```

**Delete all stashes:**

```bash
git stash clear
```

### 6. Creating a Branch from Stash

If you want to continue working on stashed changes in a new branch:

```bash
git stash branch <branch-name>
```

or with a specific stash:

```bash
git stash branch feature-new stash@{1}
```

This creates a new branch and applies the stash, then removes it from the stash list.

### 7. Practical Workflows

**Workflow 1: Switching Branches Safely**

```bash
# You're working on feature-branch with uncommitted changes
git stash

# Switch to another branch to fix an urgent bug
git checkout main

# Fix and commit the bug
git commit -m "Fix critical bug"

# Return to your feature branch
git checkout feature-branch

# Restore your work
git stash pop
```

**Workflow 2: Saving Multiple Versions**

```bash
# Save first version
git stash save "Version 1 - initial approach"

# Make different changes
# Save second version
git stash save "Version 2 - alternative approach"

# Compare by viewing both stashes
git stash show -p stash@{0}
git stash show -p stash@{1}
```

### 8. Best Practices

- Use descriptive messages when stashing (`git stash save "message"`)
- Review stashed changes before applying to avoid merge conflicts
- Use `git stash pop` if you're done with the stash, or `git stash apply` if you need it again
- Don't rely on stash for long-term storage - stashes can be accidentally lost
- For significant work-in-progress, commit to a temporary branch instead
- Regularly clean up old stashes with `git stash clear` or delete specific ones
- Use meaningful branch names when using `git stash branch`
