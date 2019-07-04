---
title: git rebase
category: git
layout: 2017/sheet
---

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
