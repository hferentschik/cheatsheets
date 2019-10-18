---
title: Git
category: tools
layout: 2017/sheet
intro: |
  Some useful git commands which for working with and on `jx` 
---

### Auto signing commits

Per repo:

```bash
> git config commit.gpgsign true
```

See also [is-there-a-way-to-autosign-commits-in-git-with-a-gpg-key](https://stackoverflow.com/questions/10161198/is-there-a-way-to-autosign-commits-in-git-with-a-gpg-key)

### GPG sign commits on a branch

All commits for the `jenkins-x/jx` repo needs to be signed-off which per default adds the _Signed-off-by_ line to the commit message including your email.

Members of the GiuHub _jenkins-x_ organisation can alternatively to signing off a commit, cryptographically sign the commits. See also GitHub's [help page](https://help.github.com/en/articles/signing-commits) on this topic. To sign a single commit you specify the `-S` option:

```bash
> git commit -S
```

In case you missed to sign a commit as part of a pull request:

```bash
> git rebase --exec 'git commit --amend --no-edit -n -S' -i master
```

### Aligning lables across repositores

```bash
> npm install -g copy-github-labels-cli
> copy-github-labels -t <token> <source-repo> <destination-repo>
```

where token is your GitHub API token.

### Git filter-branch

```bash
> git filter-branch --tree-filter 'rm -rf <file-dir-to-delete>' --prune-empty HEAD
```

### Pull tags as part of `git pull`

```bash
$ git config remote.<remote>.tagOpt --tags
```
