---
author: Artem Zhivushko
title: git.essential
create: 2024-03-27 01:09:18
tags:
  - ZeroToHero
  - DevSecOps
  - git
---

# CONFIGURING GIT

> [!tip] Set the **name** and **email** that will be associated with your commits
```bash
git config --global user.name "[name]"
git config --global user.email "[email]"
```

> [!tip] Create a shortcut for a Git command (e.g. `alias.glog "log --graph --oneline"`)
```bash
git config --global alias.[alias] [command]
```

> [!tip] Set the default text editor to use for commit messages (e.g. `vi`)
```bash
git config --global core.editor [editor]
```

> [!tip] Open the global config file in a text editor for manual editing
```bash 
git config --global --edit
```

# INITIALIZING AND CLONING

## `git init`

> [!info] **INIT**
> Инициализирует локальный репозиторий

> [!tip] Initialize an empty Git repository in the current directory
```bash
git init
```

> [!tip] Create an empty Git repo in the specified directory
```bash
git init [directory]
```

## `git clone`

> [!info] **CLONE**
> Клонирует удаленный репозиторий

> [!tip] Clone a remote Git repository from the url into a local directory
```bash
git clone [url]
```

> [!tip] Clone a remote repo into the specified local directory
```bash
git clone [url] [directory]
```

# EXAMINING LOGS

## `git log`

```bash
git log                        #Show the commit history for the current branch
git log -p                     #Show the diffs from each commit in the commit history
git log --stat                 #Show stats (files changed, insertions, deletions) for each commit
git log --oneline              #Show condensed summary of commits in one line each
git log --graph --decorate     #Draw a text based graph of commits with branch names
```

## `git diff`

```bash
git diff                        #Show unstaged file differences compared to current index
git diff --cached               #Show differences between staged changes and the last commit
git diff [commit1] [commit2]    #Show changes between two commits
```

> [!tip] Show changes made in the specified commit
```bash
git show [commit]
```

# VERSIONING FILES

> [!tip] Stage file changes to be committed
```bash
git add [file]
```

> [!tip] Commit the staged snapshot with commit message
```bash
git commit -m "[message]"
```

> [!tip] Remove file from staging index and working directory
```bash
git rm [file]
```

> [!tip] Move or rename file in Git and stage the change
```bash
git mv [file] [newpath]
```

# BRANCHING AND MERGING

## `git branch`

> [!tip] 
```bash
git branch                #List all the branches in the current repository
git branch [branch]       #Create a new branch with name [branch]
git branch -d [branch]    #Delete the local branch [branch]
```

## `git checkout`

```bash
git checkout [branch]       #Switch the current branch to [branch]
git checkout -b [branch]    #Create a new branch and switch to it
```

> [!tip] Merge the history of [branch] into the current branch
> </br>
> ```bash
> git merge [branch]
> ```

# RETRIEVING AND UPDATING REPOSITORIES

## `git fetch`

> [!tip] Fetch all branches and commits from the remote repository
> </br>
> ```bash
> git fetch [remote]
> ```

## `git pull`

```bash
git pull [remote]             #Fetch remote changes and directly merge into local repository
git pull --rebase [remote]    #Fetch remote changes and rebase onto local branch
```

## `git push`

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

# REWRITING GIT HISTORY

## `git rebase`

> [!tip] Rebase current branch onto [branch]
```bash
git rebase [branch]
```

> [!tip] Interactively rebase current branch onto [commit]
```bash
git rebase -i [commit]
```

> [!tip] Show history of Git commands for current repository
```bash
git reflog
```

## `git reset`

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

# REMOTE REPOSITORIES

> [!tip] Create remote connection with *url* and alias [name]
```bash
git remote add [name] [url]
```

# UNDOING CHANGES

> [!tip] Shows which files would be removed from working directory. Use -f option to execute clean
```bash
git clean -n
```

> [!tip] Undo changes from specified commit by creating a new commit
```bash
git revert [commit]
```

# Github

## …or create a new repository on the command line

```bash
echo "# gh_to_itacademy_zav" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:ArtZhiv/gh_to_itacademy_zav.git
git push -u origin main
```

## …or push an existing repository from the command line

```bash
git remote add origin git@github.com:ArtZhiv/gh_to_itacademy_zav.git
git branch -M main
git push -u origin main
```

# GitLab

## Git global setup

```bash
git config --global user.name "Artem Zhivushko"
git config --global user.email "zhiv-art@yandex.com"
```

## Create a new repository

```bash
git clone git@gitlab.com:zhivushko_artem/gl_to_itacademy_zav.git
cd gl_to_itacademy_zav
git switch --create main
touch README.md
git add README.md
git commit -m "add README"
git push --set-upstream origin main
```

## Push an existing folder

```bash
cd existing_folder
git init --initial-branch=main
git remote add origin git@gitlab.com:zhivushko_artem/gl_to_itacademy_zav.git
git add .
git commit -m "Initial commit"
git push --set-upstream origin main
```

## Push an existing Git repository

```bash
cd existing_repo
git remote rename origin old-origin
git remote add origin git@gitlab.com:zhivushko_artem/gl_to_itacademy_zav.git
git push --set-upstream origin --all
git push --set-upstream origin --tags
```
