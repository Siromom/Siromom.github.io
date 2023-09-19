---
sidebar_position: 2
tags: ['Wiki', 'Web', 'Client-Server']
last_update:
  date: 9/18/2022
  author: sewonkimm
---

# Request

![request](./request.png)

서버에 요청하는 방법을 알아보자!

### 전통적인 방법

초기 웹에서는 HTTP 요청 후, 페이지를 다시 불러와서 페이지를 갱신했다. 처음 웹 개발을 배우기 시작했을 때부터 데이터를 비동기적으로 받아오는 방법으로 해왔기 때문에 오히려 구현하자니 바로 떠오르지 않는다. 예를 들어 버튼을 누르면 DB에 저장된 숫자 데이터에 1을 더하고 그 값을 표시하는 페이지를 구현한다고 하면

1. 버튼을 누른다.
2. 서버에 요청을 보낸다.
3. 서버는 DB값을 업데이트한다. (아직 클라이언트는 변화가 없다)
4. 클라이언트를 새로고침한다. (변경된 DB 값을 표시한다)

이런 경우에 유저의 인터랙션이 있을 때마다 화면이 깜빡거리게 되고 편의성이 떨어진다. Ajax 방식으로 이런 문제가 개선되었다.

### Ajax

Ajax는 서버와 브라우저가 비동기적으로 데이터를 교환할 수 있도록 하는 방식이다. 페이지를 다시 불러오지 않고도 데이터를 교체할 수 있고, Lazy loading을 가능하게 하므로 초기 로딩 시간을 줄일 수 있다. Ajax 전송 기법을 사용할 땐 보통 서버 response를 JSON 형태로 받아서 처리한다.

### XMLHttpRequest

### Fetch API

### Axios
