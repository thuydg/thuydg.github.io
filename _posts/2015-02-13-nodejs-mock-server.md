---
layout: blog
title: Nodejs mock server create
category: blog
tags: [nodejs, express]
summary: How to create a mock server to test API
image: https://raw.githubusercontent.com/osser/nodejs-sample/master/images/expressjs.png
---

# What is a mockserver?

Not real server but act like a real server (often no data transfer...)

# Using NodeJs to create a mock server

## Express? what is it?

* SinatraのようなNode.jsフレームワーク
* Fast, unopinionated, minimalist web framework for Node.js <From site>

## Step1 : Installation

     $ npm install express --save

## Step2 : Create express mock server

```
app = require('express')();

app.get('/', function(req, res){
        res.send('hello world');
    });

app.listen(3000);
```

ブラウザにてhttp://localhost:3000/をアクセスすると、hello worldが表示と成功！


# Memo

1. How to get command line arguments

Standard Method (no library)
The arguments are stored in process.argv
Here is the specification form http://nodejs.org/docs/latest/api/process.html#process_process_argv
process.argv is an array containing the command line arguments. The first element will be 'node', the second element will be the name of the JavaScript file. The next elements will be any additional command line arguments.

# References

* [Using Node.js and Charles Proxy to Mock a Server API](http://chariotsolutions.com/blog/post/using-node-js-charles-proxy-mock-server-api/)
* [Api mock node module](https://www.npmjs.com/package/api-mock)
* [Express framework](http://expressjs.com/)
* [使い方のブログ](http://qiita.com/morou/items/06cbe49f64d56d31b793)
* [Using nodejs and express as mock server](https://coderwall.com/p/ss80vw/using-node-js-with-express-as-a-simple-api-mock-server)
* [Express install](http://qiita.com/pakiln/items/826a9199697576e2e24a)
* [Express API](http://expressjs.com/4x/api.html)
