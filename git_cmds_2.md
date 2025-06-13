# Essential Git Commands Reference

## Initial Setup
```bash
# Set your identity
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Check your settings
git config --list
```

## Repository Creation & Cloning
```bash
# Initialize a new repository
git init

# Clone an existing repository
git clone <repository-url>
git clone <repository-url> <directory-name>
```

## Basic Workflow Commands
```bash
# Check repository status
git status

# Add files to staging area
git add <file-name>
git add .                    # Add all files
git add *.js                 # Add all JS files
git add -A                   # Add all changes (new, modified, deleted)

# Commit changes
git commit -m "Commit message"
git commit -am "Message"     # Add and commit in one step (tracked files only)

# Push changes to remote
git push
git push origin <branch-name>
git push -u origin <branch-name>  # Set upstream branch
```

## Viewing Changes & History
```bash
# View differences
git diff                     # Working directory vs staging
git diff --staged            # Staging vs last commit
git diff HEAD                # Working directory vs last commit

# View commit history
git log
git log --oneline           # Compact view
git log --graph             # Visual graph
git log -n 5                # Last 5 commits
git log --author="Name"     # Filter by author

# Show specific commit
git show <commit-hash>
```

## Branch Management
```bash
# List branches
git branch                  # Local branches
git branch -r               # Remote branches
git branch -a               # All branches

# Create and switch branches
git branch <branch-name>    # Create branch
git checkout <branch-name>  # Switch to branch
git checkout -b <branch-name>  # Create and switch

# Modern alternative (Git 2.23+)
git switch <branch-name>
git switch -c <branch-name>

# Delete branches
git branch -d <branch-name>     # Delete merged branch
git branch -D <branch-name>     # Force delete branch
git push origin --delete <branch-name>  # Delete remote branch
```

## Merging & Rebasing
```bash
# Merge branches
git merge <branch-name>
git merge --no-ff <branch-name>  # No fast-forward merge

# Rebase
git rebase <branch-name>
git rebase -i HEAD~3        # Interactive rebase (last 3 commits)

# Abort merge/rebase
git merge --abort
git rebase --abort
```

## Remote Repository Management
```bash
# View remotes
git remote -v

# Add remote
git remote add <name> <url>
git remote add origin <repository-url>

# Fetch and pull
git fetch                   # Download changes without merging
git pull                    # Fetch and merge
git pull origin <branch-name>

# Push to remote
git push origin <branch-name>
git push --all              # Push all branches
git push --tags             # Push all tags
```

## Undoing Changes
```bash
# Unstage files
git reset <file-name>
git reset                   # Unstage all files

# Discard working directory changes
git checkout -- <file-name>
git checkout .              # Discard all changes

# Modern alternative
git restore <file-name>
git restore --staged <file-name>  # Unstage file

# Reset commits
git reset --soft HEAD~1     # Keep changes in staging
git reset --mixed HEAD~1    # Keep changes in working directory
git reset --hard HEAD~1     # Discard all changes

# Revert commits (safe for shared repositories)
git revert <commit-hash>
```

## Stashing
```bash
# Stash current changes
git stash
git stash save "Description"

# List stashes
git stash list

# Apply stash
git stash apply             # Apply latest stash
git stash apply stash@{0}   # Apply specific stash
git stash pop               # Apply and remove from stash list

# Drop stash
git stash drop stash@{0}
git stash clear             # Clear all stashes
```

## Tags
```bash
# Create tags
git tag <tag-name>          # Lightweight tag
git tag -a <tag-name> -m "Message"  # Annotated tag

# List tags
git tag
git tag -l "v1.*"           # List tags matching pattern

# Push tags
git push origin <tag-name>
git push origin --tags

# Delete tags
git tag -d <tag-name>       # Delete local tag
git push origin --delete <tag-name>  # Delete remote tag
```

## Useful Aliases
```bash
# Set up common aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'
```

## Inspection & Debugging
```bash
# Show file at specific commit
git show <commit-hash>:<file-path>

# Find when a bug was introduced
git bisect start
git bisect bad              # Current commit is bad
git bisect good <commit-hash>  # Known good commit

# Blame (see who changed what)
git blame <file-name>

# Search in history
git log --grep="search term"
git log -S "code string"    # Search for code changes
```

## Cleaning Up
```bash
# Remove untracked files
git clean -n                # Dry run
git clean -f                # Remove files
git clean -fd               # Remove files and directories

# Remove ignored files
git clean -fX
```

## Common Workflows

### Feature Branch Workflow
```bash
# Start new feature
git checkout -b feature/new-feature
# Make changes, commit
git add .
git commit -m "Add new feature"
# Push to remote
git push -u origin feature/new-feature
# Create pull request, then merge and cleanup
git checkout main
git pull origin main
git branch -d feature/new-feature
```

### Hotfix Workflow
```bash
# Create hotfix branch from main
git checkout main
git checkout -b hotfix/urgent-fix
# Make fix, commit
git add .
git commit -m "Fix urgent issue"
# Merge back to main
git checkout main
git merge hotfix/urgent-fix
git push origin main
git branch -d hotfix/urgent-fix
```

## Tips & Best Practices

- **Commit often**: Make small, focused commits with clear messages
- **Use branches**: Keep main/master stable, use feature branches
- **Pull before push**: Always pull latest changes before pushing
- **Write good commit messages**: Start with verb, keep under 50 chars for summary
- **Review before commit**: Use `git diff --staged` to review staged changes
- **Use .gitignore**: Exclude files that shouldn't be tracked
- **Backup important work**: Push to remote repository regularly
