---
layout: post
title: GET & POST
date: 2019-07-30 19:10:00
author: "SeWonKim"
categories: [Youtube Clone Coding]
tags: [jekyll, Youtube Clone Coding, Clone Coding, Nomadcoders, Express]
fullview: false
comments: true
description: How the http works?
---

![Alt text](https://i.stack.imgur.com/gNMR2.png)

Express 서버를 만들고 localhost:4000에 접속했을 때 볼 수 있는 화면      
이때 GET은 무엇일까?


## GET & POST
**GET**      
: 웹사이트에 접속하면 GET method를 이용해 서버에 request를 보내고 페이지를 받아온다.

**POST**    
: 로그인을 할 때, POST method가 브라우저에서 웹사이트로 로그인 정보를 전달해준다.


[🔗GET과 POST의 비교](https://preamtree.tistory.com/12)



## Request & Response
```javascript
function handleHome(req, res) {
    res.send('Hi from home');
}

function handleProfile(req, res) {
    res.send("You are on my profile");
}

app.get("/", handleHome);

app.get("/profile", handleProfile);
```

GET method는 request와 response를 작성해줘야한다.       
/ 로 GET request를 보내면 handleHome 함수의 response를 받아 화면에서 확인할 수 있다.


## res.render()와 res.redirect()
To render a page I use `res.render()`

그런데 join을 구현할 때, password와 password1 값이 다르면 res.render("/join")을 쓰고 값이 같으면 res.redirect("/home")을 써 준다.     
여기서 render와 redirect의 차이점은 url의 변경 여부에 있다.     
res.render()는 단순히 pug temeplate을 render해 주는 것이고, redirect는 url을 변경해주는 것이다.