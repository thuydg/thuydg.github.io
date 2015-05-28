---
layout: blog
title: Server tips
category: blog
tags: [server, tip]
summary: Server using tips
image: http://dhhp3c129bp03.cloudfront.net/wp-content/uploads/2012/02/linux4.jpg
---

# Tips

1. Pythonでローカルサーバーやる

python -m SimpleHTTPServer 8080

2. pushd/popd

* List all of directories

```
     dirs -v
RESULT:


```

* pushd to push the directory to list

     pushd "path"

* popd to return

     popd

* to return to specific

* search in directory

     grep -rnw 'directory' -e "pattern"

-r or -R is recursive, -n is line number and -w stands match the whole word. -l (letter L) can be added to have just the file name.

# Reference

* [ローカルでサーバーをたつため](http://qiita.com/higuma/items/b23ca9d96dac49999ab9)
* [Search](http://stackoverflow.com/questions/16956810/finding-all-files-containing-a-text-string-on-linux)
