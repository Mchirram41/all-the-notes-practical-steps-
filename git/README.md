# Git and GitHub Commands Explanation Guide

This section contains detailed explanations of every important Git and GitHub command used in real-time DevOps projects.

---

# 1. Initialize Git Repository

```bash id="mjlwmr"
git init
```

## Explanation

* Initializes a new Git repository.
* Creates a hidden `.git` directory.
* Starts tracking the project using Git.

## Real-Time Usage

Used when starting a new project.

---

# 2. Configure Global Username

```bash id="m00x87"
git config --global user.name "Mahesh"
```

## Explanation

* Sets Git username globally.
* Applies to all repositories in the system.

## Real-Time Usage

Used in developer laptops or personal systems.

---

# 3. Configure Global Email

```bash id="4vuxs6"
git config --global user.email "mahesh@gmail.com"
```

## Explanation

* Sets Git email globally.
* Email appears in commit history.

---

# 4. Configure Local Username

```bash id="h7b8yn"
git config --local user.name "ProjectUser"
```

## Explanation

* Sets username only for current repository.
* Overrides global username.

## Real-Time Usage

Useful when working on multiple company projects.

---

# 5. Configure Local Email

```bash id="dgrt0h"
git config --local user.email "project@gmail.com"
```

## Explanation

* Sets email only for current repository.
* Overrides global email.

---

# 6. Verify Git Configuration

```bash id="61fn50"
git config --list
```

## Explanation

Displays:

* Username
* Email
* Git settings
* Repository configuration

---

# 7. Check Git Status

```bash id="qulkj5"
git status
```

## Explanation

Shows:

* Modified files
* Staged files
* Untracked files
* Current branch

## Real-Time Usage

Used before commits to verify changes.

---

# 8. Add All Files to Staging Area

```bash id="m54g7s"
git add .
```

## Explanation

Adds:

* All modified files
* All new files
* All deleted files

to the staging area.

## Important Note

Avoid using in production projects because it may accidentally commit unwanted files.

---

# 9. Add Specific File

```bash id="7j1a4o"
git add app.py
```

## Explanation

Adds only selected file to staging area.

## Real-Time Best Practice

Preferred method in real-time projects.

---

# 10. Commit Changes

```bash id="u0lj06"
git commit -m "Added login feature"
```

## Explanation

Creates a commit in local repository.

A commit stores:

* Snapshot of changes
* Commit message
* Author details
* Commit ID

---

# 11. View Commit History

```bash id="ywfrg5"
git log
```

## Explanation

Displays:

* Commit IDs
* Commit messages
* Author details
* Commit dates

---

# 12. Compare Changes

```bash id="av8u4q"
git diff
```

## Explanation

Shows differences between:

* Working directory
* Staging area
* Previous commits

---

# 13. Remove File from Staging Area

```bash id="n17e6l"
git restore --staged app.py
```

## Explanation

Removes file from staging area without deleting changes.

## Real-Time Usage

Used when wrong file is added accidentally.

---

# 14. Restore Deleted or Modified File

```bash id="2k86cv"
git restore app.py
```

## Explanation

Restores deleted or modified content before commit.

---

# 15. View Local Branches

```bash id="6lz7f5"
git branch
```

## Explanation

Displays all local branches.

Current branch will show `*`.

Example:

```text id="jdbx9d"
* main
  develop
  feature-login
```

---

# 16. Create New Branch

```bash id="7jfe0y"
git branch feature-login
```

## Explanation

Creates a new branch from current branch.

---

# 17. Switch Branch

```bash id="8mnhfk"
git checkout feature-login
```

## Explanation

Moves from current branch to another branch.

---

# 18. Create and Switch Branch

```bash id="0vknz5"
git checkout -b feature-payment
```

## Explanation

* Creates branch
* Immediately switches to new branch

## Real-Time Usage

Most commonly used command for feature development.

---

# 19. Delete Branch

```bash id="gspw10"
git branch -d feature-login
```

## Explanation

Deletes local branch safely.

## Important Note

Merged commits remain available in main branch.

---

# 20. Rename Branch

```bash id="5s9q0y"
git branch -m old-name new-name
```

## Explanation

Renames existing branch.

---

# 21. Clone Repository

```bash id="2wyq2r"
git clone https://github.com/user/project.git
```

## Explanation

Copies remote repository into local system.

## What It Downloads

* Source code
* Branches
* Commit history
* Repository configuration

---

# 22. Fetch Remote Changes

```bash id="l0k9vk"
git fetch
```

## Explanation

Downloads latest changes from remote repository without merging.

## Real-Time Usage

Used to review changes before merging.

---

# 23. Pull Remote Changes

```bash id="lk01gj"
git pull
```

## Explanation

* Fetches remote changes
* Automatically merges changes

## Important Formula

```text id="nquu8r"
git pull = git fetch + git merge
```

---

# 24. Push Changes to Remote Repository

```bash id="lrjn1l"
git push origin feature-login
```

## Explanation

Pushes local branch changes to remote repository.

## Components

| Component     | Meaning                |
| ------------- | ---------------------- |
| git push      | Push changes           |
| origin        | Remote repository name |
| feature-login | Branch name            |

---

# 25. Merge Branches

```bash id="s3hzlv"
git merge feature-login
```

## Explanation

Combines changes from feature branch into current branch.

## Real-Time Workflow

Usually done after:

* Code review
* Testing
* Pull request approval

---

# 26. Compare Two Commits

```bash id="6djlwm"
git diff commit1 commit2
```

## Explanation

Shows differences between two commits.

---

# 27. View Connected Remote Repositories

```bash id="a0ghvz"
git remote -v
```

## Explanation

Displays connected remote repositories.

Example:

```text id="cvd4du"
origin  https://github.com/user/project.git (fetch)
origin  https://github.com/user/project.git (push)
```

---

# 28. Create Lightweight Tag

```bash id="1q6g1u"
git tag v1.0
```

## Explanation

Creates simple tag pointing to current commit.

## Real-Time Usage

Used for release versions.

---

# 29. Create Annotated Tag

```bash id="kw1flw"
git tag -a v1.0 -m "First release"
```

## Explanation

Creates annotated tag with:

* Message
* Date
* Author information

---

# 30. View Tags

```bash id="m6qjlwm"
git tag
```

## Explanation

Displays all tags.

---

# 31. Push Specific Tag

```bash id="7r6kzi"
git push origin v1.0
```

## Explanation

Pushes specific tag to remote repository.

---

# 32. Push All Tags

```bash id="s1jrd6"
git push --tags
```

## Explanation

Pushes all local tags to remote repository.

---

# 33. Delete Local Tag

```bash id="we75z4"
git tag -d v1.0
```

## Explanation

Deletes local tag.

---

# 34. Delete Remote Tag

```bash id="12al7g"
git push origin --delete v1.0
```

## Explanation

Deletes remote tag from GitHub repository.

---

# 35. Rebase Branch

```bash id="rw16v1"
git rebase main
```

## Explanation

Moves current branch commits on top of main branch.

## Benefits

* Cleaner commit history
* Linear project history

---

# 36. GitHub Pull Request (PR)

## Explanation

Pull Request is used to:

* Propose code changes
* Review code
* Merge branches safely

## Real-Time Workflow

1. Create feature branch
2. Make changes
3. Push branch
4. Raise Pull Request
5. Review changes
6. Merge after approval

---

# 37. GitHub Issues

## Explanation

GitHub Issues are used to track:

* Bugs
* Tasks
* Enhancements
* Feature requests

## Real-Time Usage

Organizations assign issues to developers.

---

# 38. Git Fork

## Explanation

Fork creates personal copy of another repository.

## Used For

* Open-source contributions
* Safe experimentation

---

# 39. Branch Protection Rules

## Explanation

Used to secure important branches like:

* main
* master

## Features

* Prevent direct pushes
* Require PR approvals
* Enforce CI/CD checks

---

# 40. Merge Conflicts

## Explanation

Merge conflicts happen when:

* Two branches modify same code lines
* Git cannot decide which change to keep

## Solution

Developers manually resolve conflicts.

---

# Real-Time Best Practices

* Avoid `git add .`
* Use feature branches
* Use Pull Requests
* Protect main branches
* Use tags for releases
* Use issues for task tracking
* Use `git fetch` before `git pull`

---

# Conclusion

Understanding Git and GitHub commands is essential for:

* DevOps Engineers
* Developers
* Cloud Engineers

These commands are heavily used in real-time project environments.
########################################################################

# Advanced Git Commands and Development Operations

This README contains advanced Git concepts and real-time development operations used in DevOps and software development projects.

---

# Topics Covered

* Git Rebase
* `.gitignore`
* Git Logs
* Git Reset
* Git Revert
* Git Commit Amend
* Git Cherry-Pick
* Git Stashing
* Git Squash

---

# 1. Git Rebase

## Definition

Git Rebase is used to move or replay commits from one branch onto another branch.

Rebasing helps maintain:

* Clean commit history
* Linear project history
* Easy-to-read Git logs

---

# Real-Time Rebase Scenario

---

## Step 1: Create Files and Commit in Master Branch

```bash id="gh0m9t"
git add .
git commit -m "Initial commit"
```

### Explanation

* Adds files to staging area
* Creates commits in master branch

---

## Step 2: Create Feature Branch

```bash id="n0osfs"
git checkout -b feature-login
```

### Explanation

* Creates new branch
* Switches to feature branch

---

## Step 3: Add Multiple Commits in Feature Branch

```bash id="8w9spg"
git add .
git commit -m "Added login page"

git add .
git commit -m "Added authentication"
```

### Explanation

Creates multiple commits inside feature branch.

---

## Step 4: Switch Back to Master Branch

```bash id="4bwp44"
git checkout master
```

### Explanation

Moves from feature branch to master branch.

---

## Step 5: Add More Commits in Master Branch

```bash id="6xxcwi"
git add .
git commit -m "Updated dashboard"
```

### Explanation

Now:

* Master branch has separate commits
* Feature branch has separate commits

Both histories are different.

---

# Why Rebase?

To maintain:

* Clean history
* Linear commit flow

---

## Step 6: Switch to Feature Branch

```bash id="o7n8eu"
git checkout feature-login
```

---

## Step 7: Rebase Feature Branch

```bash id="jx24ji"
git rebase master
```

### Explanation

* Takes feature branch commits
* Places them on top of latest master commits

---

# Result of Rebase

Before Rebase:

```text id="jq5c2o"
master -> A --- B
feature -> A --- C --- D
```

After Rebase:

```text id="11ek3z"
master -> A --- B
feature -> A --- B --- C --- D
```

---

# Benefits of Rebase

* Clean Git history
* Linear commit structure
* Easier debugging
* Better project tracking

---

# Important Note

Avoid rebasing shared/public branches because it rewrites commit history.

---

# 2. .gitignore

## Definition

`.gitignore` is a file used to tell Git which files and directories should be ignored.

Ignored files will:

* Not be tracked
* Not be pushed to repository

---

# Why Use `.gitignore`?

Used to ignore:

* Log files
* Temporary files
* Sensitive files
* Build artifacts
* Environment files

---

# Create `.gitignore` File

```bash id="k0rf3y"
touch .gitignore
```

### Explanation

Creates `.gitignore` file.

---

# Example `.gitignore`

```text id="u0c0zn"
*.txt
*.log
Mahesh/
```

### Explanation

| Pattern | Meaning                 |
| ------- | ----------------------- |
| *.txt   | Ignore all text files   |
| *.log   | Ignore all log files    |
| Mahesh/ | Ignore Mahesh directory |

---

# Important Note

`/` is mainly used for directories.

Example:

```text id="d2tviz"
logs/
```

Ignores entire logs directory.

---

# Real-Time Usage

Used for ignoring:

* `.env`
* `node_modules`
* Log files
* Temporary build files

---

# 3. Git Logs

Git logs are used to view commit history.

---

# View Full Commit History

```bash id="md5b2r"
git log
```

### Explanation

Displays:

* Commit ID
* Author
* Date
* Commit message

---

# View One-Line Commit History

```bash id="llfnpv"
git log --oneline
```

### Explanation

Displays commit history in short format.

---

# View File Change Statistics

```bash id="lfm6dn"
git log --stat
```

### Explanation

Shows:

* Modified files
* Deleted files
* Number of changes

---

# View Detailed File Differences

```bash id="0w7q0z"
git log -p
```

### Explanation

Shows detailed line-by-line changes.

---

# View Last 10 Commits

```bash id="8ln6h4"
git log -n 10
```

### Explanation

Displays last 10 commits.

---

# View Last 10 Commits in One Line

```bash id="1dlh6w"
git log -n 10 --oneline
```

---

# View Author Commit Summary

```bash id="3l4r6g"
git shortlog
```

### Explanation

Displays:

* Author names
* Number of commits

---

# View Commits by Specific Author

```bash id="89m9j7"
git log --author="mahesh@gmail.com"
```

### Explanation

Displays commits created by specific author.

---

# View Author Commits in One Line

```bash id="wjlwmn"
git log --author="mahesh@gmail.com" --oneline
```

---

# Search Commit Messages

```bash id="gvt1ey"
git log --grep="login feature"
```

### Explanation

Searches commit history using commit message.

---

# 4. Git Reset

## Definition

Git Reset is used to:

* Undo commits
* Undo staged changes
* Move commits back

---

# Soft Reset

```bash id="3mjlwm"
git reset --soft HEAD~1
```

### Explanation

* Removes latest commit
* Keeps changes staged

### Real-Time Usage

Used when:

* Commit message is wrong
* Want to recommit changes

---

# Mixed Reset (Default)

```bash id="kltqzk"
git reset HEAD~1
```

### Explanation

* Removes latest commit
* Moves changes to working directory
* Unstages changes

---

# Hard Reset

```bash id="eqlkqv"
git reset --hard HEAD~1
```

### Explanation

* Removes latest commit
* Deletes staged changes
* Deletes working directory changes

---

# Important Warning

`git reset --hard` permanently deletes uncommitted changes.

Use carefully.

---

# 5. Git Revert

## Definition

Git Revert creates a new commit that undoes previous commit changes.

---

# Why Use Revert?

Used when:

* Wrong changes already pushed
* Need safe rollback
* Want to preserve project history

---

# Revert Specific Commit

```bash id="kl2yql"
git revert <commit-id>
```

### Explanation

Creates new commit that reverses specified commit.

---

# Revert Latest Commit

```bash id="z1pb6f"
git revert HEAD
```

### Explanation

Reverts latest commit safely.

---

# Important Note

Unlike reset:

* Revert does not delete history
* Revert creates additional commit

---

# 6. Git Commit Amend

## Definition

`git commit --amend` is used to modify the latest commit.

---

# Why Use Amend?

Used for:

* Fixing commit messages
* Adding missed files
* Updating latest commit

---

# Amend Commit Message

```bash id="drm9w7"
git commit --amend -m "Updated commit message"
```

### Explanation

Changes latest commit message.

---

# Amend with Additional Files

```bash id="7qkav7"
git add app.py
git commit --amend
```

### Explanation

Adds missed files into latest commit.

---

# Real-Time Usage

Mostly used for:

* Renaming latest commit
* Adding forgotten files

---

# 7. Git Cherry-Pick

## Definition

Cherry-pick applies specific commit from one branch into another branch.

---

# Why Use Cherry-Pick?

Used when:

* Need only specific commits
* Avoid merging full branch
* Apply hotfix quickly

---

# Cherry-Pick Command

```bash id="v3y7ie"
git cherry-pick <commit-id>
```

### Explanation

Copies selected commit into current branch.

---

# Real-Time Example

Suppose:

* Feature branch has 10 commits
* Need only 1 bug fix commit

Use cherry-pick instead of merging full branch.

---

# 8. Git Stashing

## Definition

Git Stash temporarily saves uncommitted changes.

---

# Why Use Stash?

Used when:

* Need to switch branches quickly
* Work is incomplete
* Need temporary storage

---

# Real-Time Scenario

Suppose:

* Working on feature branch
* Suddenly production issue comes
* Need to switch branch immediately

Instead of committing incomplete code:

* Use stash

---

# Save Changes in Stash

```bash id="1mzv5o"
git stash
```

### Explanation

Temporarily stores:

* Working directory changes
* Staged changes

---

# View Stash List

```bash id="12v1xj"
git stash list
```

### Explanation

Displays all saved stashes.

---

# Apply Stashed Changes

```bash id="gngw0h"
git stash apply
```

### Explanation

Restores stashed changes.

---

# Apply and Remove Stash

```bash id="sh6wgp"
git stash pop
```

### Explanation

* Restores stash
* Removes stash entry

---

# Important Note

Before stashing:

* Add files properly
* Save working changes

---

# 9. Git Squash

## Definition

Squashing combines multiple commits into single commit.

---

# Why Use Squash?

Used to:

* Clean commit history
* Combine related commits
* Improve readability

---

# Real-Time Usage

Suppose feature branch contains:

```text id="2gk7ry"
Added login page
Fixed login bug
Updated login CSS
Changed login validation
```

Before merging:

* Combine into one meaningful commit

Example:

```text id="1ew33t"
Added complete login feature
```

---

# Squash Using Interactive Rebase

```bash id="3lxvx8"
git rebase -i HEAD~4
```

### Explanation

Opens interactive editor to combine commits.

---

# Benefits of Squashing

* Clean history
* Professional commit structure
* Easier code reviews

---

# Real-Time Best Practices

* Use rebase for clean history
* Use revert for safe rollback
* Avoid hard reset in production
* Use stash for temporary work
* Use squash before merging feature branches
* Use `.gitignore` properly

---

# Conclusion

These advanced Git operations are heavily used in:

* DevOps projects
* CI/CD workflows
* Team collaboration
* Production support
* Release management

Understanding these concepts is very important for real-time DevOps Engineers and Developers.
