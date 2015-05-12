---
layout: blog
title: Git study
category: blog
tags: [git]  
summary: Git study memo
image: /images/blog/git.png
---

# コミットが失敗して、やり直すか考えてた時、迷ったときのメモ

Source: http://d.hatena.ne.jp/mrgoofy33/20100910/1284069468

* 直前にしたコミットをやり直す（git commit –amend）
* コミット自体を取り消したい場合
* コミット自体を取り消しする(なかった事にする)には、「git reset」を使います。

>  「git reset」には「git reset –soft」と「git reset –hard」の2種類があります。

> 「git reset –soft」 → ワークディレクトリの内容はそのままでコミットだけを取り消す。

> 「git reset –hard」 → コミット取り消した上でワークディレクトリの内容も書き換える。

# Git branch

* ブランチをみる

```
git branch
```

* ブランチを作成したい

```
git branch ＜ブランチ名＞
```

* git 切り替え

```
git checkout <ブランチ>
```

# Git remote

     git remote add origin ...
     git remote rm origin

# Git管理

* Branch
* Tag

# Git config

* How to check

```
$ git config --list
user.name=Scott Chacon
user.email=schacon@gmail.com
color.status=auto
color.branch=auto
color.interactive=auto
color.diff=auto
...
```

* How to change

```
$ git config --global user.name "John Doe"
$ git config --global user.email johndoe@example.com
```

# Git commit delete

* revert
* cherry-pick

# git global setting ~/.gitignore

* HOME directoryに追加するための~/.gitignoreを作成,そして登録する
     $ git config --global core.excludesfile ~/.gitignore
* いつ使うかというと、MAC専用のファイル（*.DS_Storeを設定できる）

# How to rename branch on both local and remote

The closest thing to renaming is deleting and then re-creating on the remote. For example:

```
git branch -m master master-old
git push remote :master         # delete master
git push remote master-old      # create master-old on remote

git checkout -b master some-ref # create a new local master
git push remote master          # create master on remote
```

# Reference

* [サルでもわかるGit](http://www.backlog.jp/git-guide/reference/branch.html)
* [Git branching model](http://nvie.com/posts/a-successful-git-branching-model/)
