---
layout: blog
title: node modules
category: blog
tags: [nodejs, javascript]
summary: nodejs and how to use modules
image: http://calebmadrigal.com/images/nodejs-logo.png
---

# superagent:

 * What is it? a small client to access http
 * Usage: ドキュメント参考　→　[link](http://visionmedia.github.io/superagent/)

  - 簡単なリクエスト実装：

  ```
  request
  .post('/api/pet')
  .send({ name: 'Manny', species: 'cat' })
  .set('X-API-Key', 'foobar')
  .set('Accept', 'application/json')
  .end(function(err, res){
    if (res.ok) {
      alert('yay got ' + JSON.stringify(res.body));
    } else {
      alert('Oh no! error ' + res.text);
    }
  });

  ```

  requestオブジェクトのメソッドを利用して設定、.end()メソッドにより通信実施

  - リクエストの設定: GET, POST, DELETE, PUT, HEADER request:

  ```
    .get()
    OR
    .post()
    OR
    .del()
    OR
    .put()
    OR
    .header()
  ```

  - リクエストのヘッダーの設定: Using the .set() method to set parameters.

  ```
  request
   .get('/search')
   .set('API-Key', 'foobar')
   .set('Accept', 'application/json')
   .end(callback);
  ```

  - Set GET, POST data for request

  Use .query() method accepts objects to form a query-string. The following will produce the path /search?query=Manny&range=1..5&order=desc.

```
   request
     .get('/search')
     .query({ query: 'Manny' })
     .query({ range: '1..5' })
     .query({ order: 'desc' })
     .end(function(err, res){
     });
```

  Use .send() method to get json form POST data.

```
request.post('/user')
  .set('Content-Type', 'application/json')
  .send('{"name":"tj","pet":"tobi"}')
  .end(callback)
```

# bluebird:

 * What is it? a full featured promise library
 * まず、promiseは何だと？非同期処理を実はコールバックのように書けばいいが、長くなったり、わかり難いので、
 promiseを使えば、よりいい感じに書けるとのことです。
 　例：
   Before

 ```
 A(function(a){
  B(a, function(b){
    C(b, function(c){
      done(c); // ABC
    });
  });
});
 ```

   After

```
A().then(B).then(C).then(done);  // ABC
```

* Bluebirdの使い方（APIドキュメント）：https://github.com/petkaantonov/bluebird/blob/master/API.md


# Chai

* Chai is a BDD / TDD assertion library for node and the browser that can be delightfully paired with any javascript testing framework.
* The assert style is exposed through assert interface.
* How to use: [link](http://chaijs.com/guide/styles/)

```
var expect = require('chai').expect
  , foo = 'bar'
  , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.length(3);
expect(beverages).to.have.property('tea').with.length(3);
```

# Config

* Configを管理するためのモジュール
* Usage
  - Configurations file create: stored in ./config folder
  -

# Reference

* [SuperAgent](https://github.com/visionmedia/superagent)
* [Bluebird](https://github.com/petkaantonov/bluebird)
* [nodejs and promise](http://blog.otakumode.com/2014/09/17/nodejs-promise/)
