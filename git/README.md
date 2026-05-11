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
