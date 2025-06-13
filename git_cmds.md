# Git Basics - Quick Reference

## Initial Setup (One Time)
```bash
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
```

## Creating a Repository

### Start from scratch
```bash
git init
git add .
git commit -m "Initial commit"
git remote add origin <repository-url>
git push -u origin main
```

### Clone existing repository
```bash
git clone <repository-url>
```

## Basic Daily Workflow
```bash
# Check what changed
git status

# Add files to commit
git add .

# Commit changes
git commit -m "Your commit message"

# Push to remote
git push
```

## Working with Branches
```bash
# Create and switch to new branch
git checkout -b <branch-name>

# Switch between branches
git checkout <branch-name>

# Push new branch to remote
git push -u origin <branch-name>

# Merge branch into main
git checkout main
git merge <branch-name>
```

## Getting Latest Changes
```bash
# Get latest changes from remote
git pull

# Or step by step
git fetch
git merge
```

## Forking Workflow
```bash
# 1. Fork on GitHub/GitLab (use web interface)
# 2. Clone your fork
git clone <your-fork-url>

# 3. Add original repo as upstream
git remote add upstream <original-repo-url>

# 4. Keep your fork updated
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

## Undo Common Mistakes
```bash
# Undo last commit (keep changes)
git reset --soft HEAD~1

# Discard all local changes
git checkout .

# Remove file from staging
git reset <filename>
```

## Essential Commands Summary
- `git init` - Create new repository
- `git clone` - Copy repository from remote
- `git add` - Stage files for commit
- `git commit` - Save changes with message
- `git push` - Send changes to remote
- `git pull` - Get latest changes from remote
- `git status` - Check current state
- `git checkout -b` - Create and switch to new branch
