---
author: Artem Zhivushko
title: git.essential
create: 2024-03-27 01:09:18
tags:
  - ZeroToHero
  - DevSecOps
  - git
---
# Git Cheat Sheet

## GIT BASICS & CONFIG

### `git init`

> [!info] Create empty Git repo in specified directory. Run with no arguments to initialize the current directory as a git repository.

```bash
git init [directory]
```

### `git clone`

> [!info] Clone repo located at [repo] onto local machine. Original repo can be located on the local filesystem or on a remote machine via HTTP or SSH.

```bash
git clone [url]
git clone [url] [directory]
```

### `git config`

#### git config levels and files

> [!warning] Thus the order of priority for configuration levels is: **local**, **global**, **system**. This means when looking for a configuration value, Git will start at the local level and bubble up to the system level.

- `--local`

> [!info] By default, `git config` will write to a local level if no configuration option is passed. Local level configuration is applied to the context repository `git config` gets invoked in. Local configuration values are stored in a file that can be found in the repo's .git directory: `.git/config`

- `--global`

> [!info] Global level configuration is user-specific, meaning it is applied to an operating system user. Global configuration values are stored in a file that is located in a user's home directory. `~ /.gitconfig` on unix systems and `C:\Users\\.gitconfig` on windows

- `--system`

> [!info] System-level configuration is applied across an entire machine. This covers all users on an operating system and all repos. The system level configuration file lives in a `gitconfig` file off the system root path. `$(prefix)/etc/gitconfig` on unix systems. On windows this file can be found at `C:\Documents and Settings\All Users\Application Data\Git\config` on Windows XP, and in `C:\ProgramData\Git\config` on Windows Vista and newer.

#### examples of commands

> [!info] Set the **name** and **email** that will be associated with your commits

```bash
git config --global user.name "[name]"
git config --global user.email "[email]"
```

> [!info] Create a shortcut for a Git command (e.g. `alias.glog "log --graph --oneline"`)

```bash
git config --global alias.[alias] [command]
```

> [!info] Set the default text editor to use for commit messages (e.g. `vi`)

```bash
git config --global core.editor [editor]
```

> [!info] Open the global config file in a text editor for manual editing

```bash 
git config --global --edit
```

### `git add`

> [!info] Stage all changes in [directory] for the next commit. Replace [directory] with a [file] to change a specific file.

```bash
git add [file]
git add [directory]
```

Start an interactive indexing session, during which you can select the parts of the file that will be added to the next commit. The command will present a fragment of the changes and prompt you to enter a command. Enter:
- `y` to index the fragment; 
- `n` to ignore the fragment; 
- `s` to break it into smaller fragments; 
- `e` to manually edit the fragment; 
- `q` to complete the command.

```bash
git add -p
```

### `git commit`

> [!info] Commit the staged snapshot, but instead of launching a text editor, use [message] as the commit message.

```bash
git commit -m "[message]"
```

### `git status`

> [!info] List which files are staged, unstaged, and untracked.

### `git log`

> [!info] Display the entire commit history using the default format. For customization see additional options.

```bash
git log                      # Show the commit history for the current branch
git log -p                   # Show the diffs from each commit in the commit history
git log --stat               # Show stats (files changed, insertions, deletions) for each commit
git log --oneline            # Show condensed summary of commits in one line each
git log --graph --decorate   # Draw a text based graph of commits with branch names
```

### `git diff`

> [!info] Show unstaged changes between your index and working directory.

```bash
git diff                      # Show unstaged file differences compared to current index
git diff --cached             # Show differences between staged changes and the last commit
git diff [commit1] [commit2]  # Show changes between two commits
```
## UNDOING CHANGES

### `git revert`

> [!info] Create new commit that undoes all of the changes made in [commit], then apply it to the current branch.

```bash
git revert [commit]
```

### `git reset`

> [!info] Remove [file] from the staging area, but leave the working directory unchanged. This unstages a file without overwriting any changes.

> [!faq] Сравнительная таблица режимов:
> 
> Пример ветки репозитория:  
> `- A - B - C (master)`  
> **HEAD** указывает на **C** и индекс совпадает с **C**.
> 
> > [!info] Выполнив: `git reset --soft B`
> > HEAD будет указывать на **B** и изменения из коммита **C** будут в индексе, как будто были добавлены командой `git add`.
> > Если вы сейчас выполнить `git commit` получим коммит полностью идентичный **C**.
> 
> > [!info] Выполнив `git reset --mixed B` или `git reset B`
> > **HEAD** вновь указывает на **B**, но на этот раз изменения из **С** не будут в индексе и если запустить `git commit` ничего не произойдет т.к. ничего нет в индексе.
> > Все изменения из **С** есть, но если запустить `git status` то в выводе будет, что все изменения *not staged*.
> > Чтобы их закоммитить нужно сначала добавить их в индекс командой `git add` и только после этого `git commit`.
> 
> > [!info] Выполнив `git reset --hard B`
> > Последний режим `--hard` также как и `--mixed` переместит **HEAD** на **В** и очистит индекс, но в отличие от `--mixed` жесткий `reset` *изменит файлы в вашей рабочей директории*. 
> > При использовании данного режима изменения из **С**, равно как и незакоммиченные изменения, будут удалены и файлы в репозитории будут совпадать с **B**.
> > > [!critical] Учитывая то, что этот режим подразумевает потерю изменений, **всегда** нужно проверять `git status` перед тем как выполнить жесткий `reset` чтобы убедиться что нет незакоммиченных изменений (или они не нужны).
> 
> | | меняет индекс | меняет файлы в рабочей директории | нужно быть внимательным |
> |---|---|---|---|
> |`reset --soft`|нет|нет|нет|
> |`reset [--mixed]`|да|нет|нет|
> |`reset --hard`|да|да|да|

> [!tip] clear staging area, rewrite working tree from specified commit

```bash
git reset --hard [commit]
```

> [!tip] Remove file from staging index but leave unchanged Iocally

```bash
git reset [file]
```

### `git clean`

> [!info] Shows which files would be removed from working directory. Use the `-f` flag in place of the `-n` flag to execute the clean.

```bash
git clean -f
git clean -n
```

## REWRITING GIT HISTORY

### `git commit`

> [!info] Replace the last commit with the staged changes and last commit combined. Use with nothing staged to edit the last commit’s message.

```bash
git commit --amend
```

### `git rebase`

> [!info] Rebase the current branch onto [base]. [base] can be a commit ID, branch name, a tag, or a relative reference to `HEAD`.

```bash
git rebase [branch]
git rebase -i [commit] # Interactively rebase current branch onto [base]. Launches editor to enter commands for how each commit will be transferred to the new base.
```

### `git reflog`

> [!info] Show a log of changes to the local repository’s `HEAD`. Add `--relative-date` flag to show date info or `--all` to show all refs.

## GIT BRANCHES

### `git branch`

> [!info] List all of the branches in your repo. Add a [branch] argument to create a new branch with the name [branch].

```bash
git branch                # List all the branches in the current repository
git branch [branch]       # Create a new branch with name [branch]
git branch -d [branch]    # Delete the local branch [branch]
```

### `git checkout`

> [!info] Create and check out a new branch named [branch]. Drop the `-b` flag to checkout an existing branch.

```bash
git checkout [branch]
git checkout -b [branch]
```

### `git merge`

> [!info] Merge [branch] into the current branch.

```bash
git merge [branch]
```

## REMOTE REPOSITORIES

### `git remote`

> [!info] Create a new connection to a remote repo. After adding a remote, you can use [name] as a shortcut for [url] in other commands.

```bash
git remote add [name] [url]
```

### `git fetch`

> [!info] Fetches a specific [branch], from the repo. Leave off [branch] to fetch all remote refs.

```bash
git fetch [remote] [branch]
```

### `git pull`

> [!info] Fetch the specified remote’s copy of current branch and immediately merge it into the local copy.

```bash
git pull [remote]             # Fetch remote changes and directly merge into local repository
git pull --rebase [remote]    # Fetch the remote’s copy of current branch and rebases it into the local copy. Uses git rebase instead of merge to integrate the branches.
```

### `git push`

> [!info] Push the branch to [remote], along with necessary commits and objects. Creates named branch in the remote repo if it doesn’t exist.

> [!tip] Push local branch to remote repository

```bash
git push [remote] [branch]
```

> [!tip] Push all local branches to remote

```bash
git push --all [remote]
```

> [!tip] Push all local tags to remote repository

```bash
git push --tags [remote]
```

> [!tip] Forces the git push even if it results in a non-fast-forward merge. Do not use the `--force` flag unless you’re absolutely sure you know what you’re doing.

```bash
git push [remote] --force
```

## `git diff`

```bash
git diff HEAD       # Show difference between working directory and last commit.
git diff --cached   # Show difference between staged changes and last commit
```

## GIT LOG

### `git log`

```bash
git log -[limit]               # Limit number of commits by [limit]. E.g. ”git log -5” will limit to 5 commits.
git log --author="[pattern]"   # Search for commits by a particular author.
git log --grep="[pattern]"     # Search for commits with a commit message that matches [pattern].
git log [since]..[until]       # Show commits that occur between [since] and [until]. Args can be a commit ID, branch name, HEAD, or any other kind of revision reference.
git log -- [file]              # Only display commits that have the specified file.
```

### `git show`

> [!info] Show changes made in the specified commit

```bash
git show [commit]
```
