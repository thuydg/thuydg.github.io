---
layout: blog
title: To write jekyll blog beautifully and easily
category: blog
tags: [jekyll]
summary: Jekyll blog writing technique and more
image: http://wolfslittlestore.be/wp-content/uploads/2013/07/jekyll.png
---

## How to write?

Here is some good summarize.

    #、##、###：見出し
    見出し文字の下に「=====」(h1)「-----」(h2)でもいい
    *ABCDEFG*：斜体
    **ABCDEFG**：強調
    「*」「+」「-」：箇条書き（記号の直後にスペースかタブ要）
    行頭に数字＋ピリオド：番号付け（記号の直後にスペースかタブ要）
    箇条書き・番号付けの後ろで改行は、「行末スペース*2」でできる
    レベル2は、「 - 」。
    >：引用
    [リンクテキスト](URL "タイトル")：リンク
    ![代替テキスト](画像のURL)：画像
    行末にスペース2つ：段落内での改行
    行頭にスペース4つ またはタブ：コードの記述
    HTMLタグ：直接タグを書く(一部制限あり)

* Table


    | Left align | Right align | Center align |
    |:-----------|------------:|:------------:|
    | This       |        This |     This     |
    | column     |      column |    column    |
    | will       |        will |     will     |
    | be         |          be |      be      |
    | left       |       right |    center    |
    | aligned    |     aligned |   aligned    |


* バックスラッシュ[\]をMarkdownの前に挿入することで、Markdownをエスケープ(無効化)することができます。

## Cheatsheet

![Cheat-sheet](/images/blog/markdown_cheatsheet.jpg)

## How to write code in Jekyll

Jekyll also has built-in support for syntax highlighting of code snippets using either Pygments or Rouge, and including a code snippet in any post is easy. Just use the dedicated Liquid tag as follows:

{% highlight ruby %}
    def show
      @widget = Widget(params[:id])
      respond_to do |format|
        format.html # show.html.erb
        format.json { render json: @widget }
      end
    end
{% endhighlight %}

Result:

{% highlight ruby %}
def show
  @widget = Widget(params[:id])
  respond_to do |format|
    format.html # show.html.erb
    format.json { render json: @widget }
  end
end
{% endhighlight %}

* For line number:
You can make code snippets include line-numbers by adding the word linenos to the end of the opening highlight tag like this:  [highlight ruby linenos].


## References

* [Markdownまとめ](http://www.catch.jp/wiki/index.php?markdown)
* [Cheatsheets](http://packetlife.net/library/cheat-sheets/)
* [Jekyll how to write post](http://jekyllrb.com/docs/posts/)
