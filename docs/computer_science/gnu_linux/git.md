---
title: git
date: 2017-10-25
tags: [ 'git', 'github', 'versions', 'branches' ]
---

# Configuration

## New repo

After running `git init`:

* `git config user.name "[username]"`
* `git config user.email "[email]"`
* `git config user.signingkey "[key ID]"`
* `git remote add origin [remote origin]`
* `git push -u origin [branch]`

## Autosign commits

Add the following lines to *.git/config*:

```
[commit]
    gpgsign = true
```

## Global .gitignore file

`git config --global core.excludesfile ~/.gitignore_global`

[github-help](https://help.github.com/articles/ignoring-files/)

## Hooks

### pre-commit

[pre-commit/pre-commit](https://github.com/pre-commit/pre-commit) is a
framework for managing and maintaining multi-language pre-commit hooks.

#### Usage

##### Skip specific hooks

```bash
SKIP=no-commit-to-branch pre-commit run --all-files
```

Which is useful if a CI runs for the main branch so that it doesn't complain
about running in it.

# Usage

## Cloning

### Clone a repo and its submodules

```bash
git clone --recurse-submodules -j8 [repo]
```

The `-jN` option to fetch `N` submodules at parallel.

For pulling the command is similar: `git pull --recurse-submodules`


* [stackoverflow](https://stackoverflow.com/questions/3796927/how-to-git-clone-including-submodules)
* [stackoverflow](https://stackoverflow.com/questions/1030169/easy-way-to-pull-latest-of-all-git-submodules)

## Branches

### Create new branch and switch to it

`git checkout -b [branch name]`

### Delete branchs

To delete a local branch: `git branch -d [branch]`.

To delete a remote branch: `git push origin --delete [branch]`

[makandracards](https://makandracards.com/makandra/621-git-delete-a-branch-local-or-remote)

### Rename branch

```bash
git branch -m [old_branch_name] [new_branch_name]
```

### Fetch and track remote branches

You need to create a local branch that tracks a remote branch.

```bash
git checkout --track origin/[branch_name]
```

* [Git fetch remote branch - Stack Overflow](https://stackoverflow.com/questions/9537392/git-fetch-remote-branch)

## Commits

### Revert last public commit

`git revert HEAD`

[stackoverflow](https://stackoverflow.com/questions/927358/how-to-undo-the-last-commits-in-git)

### Revert public merge commit

1. Reset to the last good commit: `git reset [commit]`
2. Set everything as it was then: `git reset --hard`
3. Force push: ` git push -f origin [branch]`

[stackoverflow](https://stackoverflow.com/questions/7099833/how-to-revert-a-merge-commit-thats-already-pushed-to-remote-branch)

### Delete last commit

`git reset HEAD^` **Note**: this won't delete the changes made, just the commit.
Also it will unstage the modified files.

[stackoverflow](https://stackoverflow.com/questions/37420642/how-to-undo-the-last-commit-in-git)

### Revert to a particular commit

`git reset --hard [commit-id]` This will remove local changes.

* [stackoverflow](https://stackoverflow.com/questions/4114095/how-do-i-revert-a-git-repository-to-a-previous-commit)

### Reset file to specific revision

To reset a file to its state in a specific commit:

`git checkout [commit-id] -- [files...]`

To revert changes made to a file in a commit (reset file to its version in the
immediately previous commit:

`git checkout [commit-id]~1 -- [files...]`

[stackoverflow](https://stackoverflow.com/questions/215718/reset-or-revert-a-specific-file-to-a-specific-revision-using-git)

### Removing sensitive data from a repository

If you commit sensitive data, such as a password or SSH key into a git
repository, you can remove it from the history. To entirely remove unwanted
files from a repository's history you can use `git filter-branch`.

To force git to process the entire history of every branch and tag
and remove the specified file as well as any empty commits generated as a result
run:

```bash
git filter-branch --force --index-filter \
  "git rm --cached --ignore-unmatch {{path_to_file}}" \
  --prune-empty --tag-name-filter cat -- --all
```

*Note*: If the file with sensitive data used to exist at any other paths
(because it was moved or renamed), you must run this command on those paths,
as well.

### GPG signed commits

#### Sign last commit

`git commit -S --amend`

### Rewrite old commits

#### Change last commit message

To edit the message: `git commit --amend`

Then to push it to the upstream: `git push --force`

[github-help](https://help.github.com/articles/changing-a-commit-message/)

#### Change author username and email

Create an alias in *.gitconfig*:
`change-commits = "!f() { VAR=$1; OLD=$2; NEW=$3; shift 3; git filter-branch --env-filter \"if [[ \\\"$`echo $VAR`\\\" = '$OLD' ]]; then export $VAR='$NEW'; fi\" $@; }; f "`

Then from the repo:

`git change-commits GIT_AUTHOR_NAME "old name" "new name"`
`git change-commits GIT_AUTHOR_EMAIL "old email" "new email"`

[stackoverflow](https://stackoverflow.com/questions/750172/change-the-author-and-committer-name-and-e-mail-of-multiple-commits-in-git)

## Files

### Untrack file/folder but keep locally

It is a good idea to add the file/folder's path to *.gitignore*. Then, to
remove the file/folder and its contents from git
tracking: `git rm [-r] --cached {path}`.

[stackoverflow](https://stackoverflow.com/questions/24290358/remove-a-folder-from-git-tracking)

## Tags

### Tag current HEAD with a message and GPG sign it

`git tag -a [tag] -m "[tag message]" -s`

Then, push it with: `git push origin [tag]`.

[git-doc](https://git-scm.com/book/en/v2/Git-Basics-Tagging)

## Delete a tag local and remote

```bash
git push --delete origin [tagname]
git tag --delete [tagname]
```

* [stackoverflow](https://stackoverflow.com/questions/5480258/how-to-delete-a-remote-tag)

## Syncing a fork

Sync a fork of a repository to keep it up-to-date with the upstream repository.

```bash
git fetch upstream
git checkout master
git merge upstream/master
```

* [GitHub Help](https://help.github.com/en/articles/syncing-a-fork)

# Tips

## Unstage files

`git reset [file]`

[stackoverflow](https://stackoverflow.com/questions/348170/how-to-undo-git-add-before-commit)

# Debug

## Failed to delete remote branch (deletion of the current branch prohibited)

The default branch must be changed from the web repo configuration.

[stackoverflow](https://stackoverflow.com/questions/14040754/deleting-remote-master-branch-refused-due-to-being-current-branch)

# Reference

## Merging

### mergetool

* [rosipov](http://www.rosipov.com/blog/use-vimdiff-as-git-mergetool/)

## Workflow

* [git-scm](https://git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)

## Commits

### Style

* [semantic commit messages](https://seesparkbox.com/foundry/semantic_commit_messages)

## Subtrees

* [atlassian](https://www.atlassian.com/blog/git/alternatives-to-git-submodule-git-subtree)

## Tips

### Usuful .gitignore

[github](https://gist.github.com/octocat/9257657)
