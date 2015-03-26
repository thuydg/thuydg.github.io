---
layout: blog
title: sublime
category: blog
tags: [javascript, maintainable]
summary: how I applied what I learnt from maintable Javascript
image: http://js.marooon.com/wp-content/uploads/2015/01/javascript_2.jpg
---


# Chapter3: Statements and Expressions (文と式)

* きれいな書き方は以下のようになりますので、積極的に使いたい

  - {}があった方が分かりやすい
  - indent注意するべき
    - if
    - for
    - while
    - do .. while
    - try .. catch .. finally

```
// Good
if (condition) {
　　doSomething();
}

```

## 3.1. Brace alignment

* はやっているスタイルは二つがあるが、JavaスタイルとC#スタイル、Javaスタイルの方がおすすめなので、
Javaスタイルを使おうかと思います。

* Javaスタイル

```
if (condition) {
  doSomething();
} else {
  doSomethingElse();
}
```

* C＃スタイル

```
if (condition)
{
  doSomething();
}
else
{
  doSomethingElse();
}
```

And when we add the Space, here is a good style that is recommended by author.

```
if (condition) {
  doSomething();
}
```

## Switch

There are many style but this one is the most suitable style that we can write
Here is the Java style.

```
switch(condition) {
    case "first":
        // code
        break;
    case "second":
        // code
        break;
    case "third":
        // code
        break;
    default:
        // code
}
```
Note that if you don't write "break;" at the end of the "case" process, it would lead to a "Fall through".
About the Default, the author suggests that we should obmit it by not including extra Default like this.

```
switch(condition) {
    case "first":
        // code
        break;
    case "second":
        // code
        break;
    // no default
}
```

## with Statement

withは変数をinterpretするコンテキストを変更する。特定オブジェクトのプロパティとメソッドを
ローカルとしてアクセス許可する。以下の本のサンプルです。

```
var book = {
    title: "Maintainable JavaScript",
    author: "Nicholas C. Zakas"
};

var message = "The book is ";
with (book) {
    message += title;
    message += " by " + author;
}
```

## The For Loop

* Traditional For loop

```
var values = [ 1, 2, 3, 4, 5, 6, 7 ],
    i, len;
for (i=0, len=values.length; i < len; i++) {
    process(values[i]);
}
```

* Break: loopを壊す

```
var values = [ 1, 2, 3, 4, 5, 6, 7 ],
    i, len;
for (i=0, len=values.length; i < len; i++)
{
    if (i == 2) {
        break; // no more iterations
    }
    process(values[i]);
}
```

* Continue: スキップする

```
var values = [ 1, 2, 3, 4, 5, 6, 7 ],
    i, len;

for (i=0, len=values.length; i < len; i++) {
    if (i == 2) {
        continue; // skip just this iteration
    }
    process(values[i]);
}
```

* For-In loop

It is used to iterate over properties of an object.
The llop goes through each named object property and return the property name inside of a variable.
  - It returns not only instance properties but all properties it inherits through the prototype.
  - It is not good to use to iterate over members of an Array because its potential errors.

```
var prop;
for (prop in object) {
    if (object.hasOwnProperty(prop)) {
        console.log("Property name is " + prop);
        console.log("Property value is " + object[prop]);
    }
}
```


# Reference:

* Maintainable Javascript - Nicholas C.Zakas
