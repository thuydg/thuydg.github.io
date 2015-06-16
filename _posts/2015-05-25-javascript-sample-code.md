---
layout: blog
title: Javascript sample code
category: blog
tags: [javascript, oop]
summary: Javascript sample code
image: http://i.ytimg.com/vi/coIsvOMYEi0/hqdefault.jpg
---

# Condition

     x = (numberOne == 1) ? true : false;

Normal one:

　　  if(numberOne == 1){
　　　　  x = true;
　　  }else{
　　　　  x = false;
　　  }

# map() function

How to write?
     arr.map(callback[, thisArg]);
How to run?
      var numbers = [1, 4, 9];
      var roots = numbers.map(Math.sqrt);
      // roots   の内容は [1, 2, 3] となる
      // numbers の内容は [1, 4, 9] のまま

# Reference

* (Map javascript)[https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/map]
