# CORE CONCEPTS
Git: Distributed Version Control System (DVCS) for tracking changes in files

Repository: Database containing project files and revision history

Three States: Working Directory → Staging Area (Index) → Repository (.git folder)

Commit: Snapshot of staged changes with metadata (author, timestamp, message)

Branch: Movable pointer to a specific commit, enabling parallel development

# LOCAL REPOSITORY WORKFLOW
# Initialization & Configuration

git init                                   # Initialize new repository
git init <directory-name>                  # Initialize in specific directory
git config --global user.name "Your Name"  # Configure user
git config --global user.email "your.email@example.com"
git config --list                          # View configuration
git config user.name                       # Check specific setting

git branch --set-upstream-to=origin/branchName    # allow our local branch to automatically attract a specific remote   branch, for example if we set the upstream to only frontend branch git pull and git push only works there and not other branches and github will know of that fact

# Basic Local Commands

git status                            # Show working tree status
git status -s                         # Short format
git log                               # Show commit history
git log --oneline                     # Compact history
git log --graph --oneline             # Visual branch history
git add <file>                        # Stage specific file
git add .                             # Stage all changes (current directory)
git add -A                            # Stage all changes (entire repo)
git add *.js                          # Stage with pattern matching
git add -p                            # Interactive staging (patch mode)
git commit                            # Opens editor for commit message
git commit -m "Descriptive message"   # Direct commit with message
git commit -am "Message"              # Add ALL tracked files and commit
git commit --amend                    # Modify last commit (message/content)
git commit --amend --no-edit          # Add changes to last commit, keep message

# Ignoring Files

touch .gitignore                      # Create .gitignore file
# Common .gitignore patterns:
# node_modules/      # Ignore entire directory
# *.log              # Ignore all .log files
# .env               # Ignore environment files
# .DS_Store          # Mac system file
# dist/              # Build output

# BRANCHING WORKFLOW
# Branch Operations

git branch                            # Local branches
git branch -a                         # All branches (including remote)
git branch -r                         # Remote branches only
git branch <branch-name>              # Create branch
git checkout <branch-name>            # Switch to branch
git checkout -b <branch-name>         # Create AND switch (combined)
git switch <branch-name>              # Newer alternative to checkout
git switch -c <branch-name>           # Create and switch (new syntax)
git branch -d <branch-name>           # Safe delete (merged only)
git branch -D <branch-name>           # Force delete (unmerged)
git push origin --delete <branch>     # Delete remote branch
git branch -m <new-name>              # Rename current branch
git branch -m <old> <new>             # Rename specific branch

# Merging & Rebasing

git checkout main                     # Switch to target branch
git merge <feature-branch>            # Merge into current branch
git merge --no-ff <branch>            # Always create merge commit
git merge --squash <branch>           # Squash all commits into one
git checkout feature
git rebase main                       # Reapply commits on top of main
git rebase -i HEAD~3                  # Interactive rebase (last 3 commits)
git merge --abort                     # Cancel merge
git rebase --abort                    # Cancel rebase
git add <resolved-file>               # Mark conflict as resolved

# REMOTE REPOSITORY WORKFLOW
# Remote Operations

git clone <url>                       # Clone into current directory
git clone <url> <folder>              # Clone into specific folder
git clone --depth=1 <url>             # Shallow clone (history truncated)
git remote -v                         # List remotes
git remote add origin <url>           # Add remote
git remote remove origin              # Remove remote
git remote rename <old> <new>         # Rename remote
git remote show origin                # Show remote details
git push                              # Push current branch to upstream
git push origin <branch>              # Push specific branch
git push -u origin <branch>           # Push AND set upstream (tracking)
git push origin --all                 # Push all branches
git push --force                      # Force push (CAUTION!)
git push --force-with-lease           # Safer force push
git fetch                             # Download objects/refs from remote
git fetch origin                      # Fetch from specific remote
git fetch --prune                     # Remove outdated remote references
git pull                              # Fetch + merge (git fetch + git merge)
git pull --rebase                     # Fetch + rebase
git pull origin main                  # Pull specific branch

# Synchronization Workflow

git fetch origin                      # Get latest from remote
git merge origin/main                 # Merge into current branch
# OR
git rebase origin/main                # Rebase on latest remote

# ADVANCED OPERATIONS
# Undoing Changes

git reset <file>                      # Unstage specific file (keep changes)
git reset                             # Unstage all files
git checkout -- <file>                # Restore file to last commit
git restore <file>                    # Newer alternative
git clean -fd                         # Remove untracked files/dirs
git clean -fdn                        # Dry run (show what would be removed)
git reset --soft HEAD~1               # Undo commit, keep changes staged
git reset --mixed HEAD~1              # Undo commit, keep changes unstaged (default)
git reset --hard HEAD~1               # Undo commit, discard changes
git reset --hard origin/main          # Match remote exactly
git revert <commit-hash>              # Create new commit that undoes changes
git revert HEAD                       # Revert latest commit

# Stashing

git stash                             # Stash changes
git stash save "Work in progress"     # Stash with message
git stash list                        # List stashes
git stash apply                       # Apply latest stash (keep in list)
git stash pop                         # Apply and drop latest stash
git stash drop stash@{0}              # Delete specific stash
git stash clear                       # Delete all stashes
git stash branch <name>               # Create branch from stash

# Viewing History & Diffs

git diff                              # Unstaged vs staged
git diff --staged                     # Staged vs last commit
git diff HEAD                         # Working vs last commit
git diff <commit1> <commit2>          # Between two commits
git diff <branch1>..<branch2>         # Between branches
git log --grep="search term"          # Search commit messages
git log -S"function_name"             # Search code changes
git log --since="2023-01-01"
git log --author="name"
git show <commit-hash>                # Show commit details

# TEAM COLLABORATION WORKFLOW
# Standard Team Workflow

# 1. Start fresh each day
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/description

# 3. Develop with regular commits
git add .
git commit -m "feat: add login component"

# 4. Keep branch updated
git fetch origin
git rebase origin/main               # OR merge, depending on team preference

# 5. Push to remote
git push -u origin feature/description

# 6. Create Pull Request on GitHub/GitLab
# 7. After PR approval and merge:

# 8. Clean up locally
git checkout main
git pull origin main
git branch -d feature/description

# Pull Request/Merge Request Workflow

# Prepare branch for PR
git checkout feature-branch
git fetch origin
git rebase origin/main               # Clean linear history
git push --force-with-lease          # Update remote branch

# After PR merge
git checkout main
git pull origin main                 # Fetch merged changes
git branch -d feature-branch         # Delete local branch
git fetch --prune                    # Clean up remote references

# WORKFLOW EXAMPLES
# Complete Development Cycle

# Initialize local repository
git init
git add .
git commit -m "Initial commit"

# Connect to remote (GitHub/GitLab)
git remote add origin https://github.com/username/repo.git
git push -u origin main

# Daily development workflow
git checkout main
git pull origin main
git checkout -b feature/new-feature
# ... make changes ...
git add .
git commit -m "feat: implement new feature"
git push -u origin feature/new-feature
# Create PR, get approval
# After merge:
git checkout main
git pull origin main
git branch -d feature/new-feature

# Cloning & Contributing

# Clone existing repository
git clone https://github.com/username/repo.git
cd repo

# Create your feature branch
git checkout -b your-feature

# Make changes and commit
git add .
git commit -m "feat: your contribution"

# Push to remote
git push origin your-feature
# Create Pull Request via GitHub/GitLab UI

# Emergency Hotfix Workflow

git checkout main
git pull origin main
git checkout -b hotfix/critical-issue
# ... fix the issue ...
git add .
git commit -m "fix: resolve critical issue"
git push origin hotfix/critical-issue
# Create PR, get immediate approval, merge
git checkout main
git pull origin main
git branch -d hotfix/critical-issue

# BEST PRACTICES & CONVENTIONS

# Commit Message Convention

feat:     New feature
fix:      Bug fix
docs:     Documentation changes
style:    Formatting, missing semi-colons, etc.
refactor: Code restructuring
test:     Adding tests
chore:    Build process, tooling changes

# Branch Naming Convention

feature/login-authentication
bugfix/header-overflow
hotfix/critical-security-patch
release/v1.2.0
docs/update-readme

# Golden Rules

1. Always pull before starting work

2. Create branches for all features/bugfixes

3. Commit often with descriptive messages

4. Never force push to shared branches (main, develop)

5. Test before pushing to remote

6. Keep main branch always deployable

7. Use .gitignore for generated files

8. Regularly fetch and prune outdated references

# TROUBLESHOOTING

# Common Issues                        Solutions

# Accidentally committed to wrong branch
git log --oneline                      # Get commit hash
git reset HEAD~1                       # Remove commit (keeps changes)  
git stash                              # Stash changes
git checkout correct-branch
git stash pop
git add .
git commit -m "message"

# Wrong commit message
git commit --amend                     # Edit last commit message

# Need to undo pushed commit
git revert <commit-hash>               # Preferred: creates undo commit
# OR (if no one else pulled)
git reset --hard HEAD~1
git push --force-with-lease

# Merge conflicts
git status                             # See conflicted files
# Edit files to resolve conflicts
git add <resolved-file>
git commit                             # Complete merge

# Recovery Commands

# Find lost commits
git reflog                            # Show ALL actions
git checkout <hash-from-reflog>       # Recover commit

# Undo almost anything (within 30 days)
git reflog
git reset --hard HEAD@{1}

# Reset to match remote exactly
git fetch origin
git reset --hard origin/main
git clean -fd                         # Remove untracked files

# QUICK REFERENCE - DAILY COMMANDS

# Morning Routine
git status
git checkout main
git pull --rebase

# Development Session
git checkout -b feature/task-name
# ... work ...
git add .
git commit -m "type: description"
git push -u origin feature/task-name

# End of Day
git stash                    # If not ready to commit
git checkout main           # Switch back to main

# Essential Aliases (add to ~/.gitconfig)

[alias]
  co = checkout
  br = branch
  ci = commit
  st = status
  lg = log --oneline --graph --all
  last = log -1 HEAD
  unstage = reset HEAD --
  undo = reset --soft HEAD~1
  who = shortlog -s -n       # Show contributors

# PRO TIPS

1. Use git add -p for granular staging (review changes before committing)

2. Always git pull --rebase to maintain linear history

3. Commit messages should complete "This commit will..."

4. Use feature flags instead of long-lived branches

5. Regularly run git gc to optimize repository

6. Set up pre-commit hooks for code quality

7. Use SSH keys instead of HTTPS for authentication

8. Configure git autocomplete for faster command line work

