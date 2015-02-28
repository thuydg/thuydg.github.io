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

# Reference

* [サルでもわかるGit](http://www.backlog.jp/git-guide/reference/branch.html)
