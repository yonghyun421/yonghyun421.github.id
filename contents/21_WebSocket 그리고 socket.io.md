---
date: '2021-11-14'
title: 'WebSocket 그리고 socket.io'
categories: ['React', 'TIL', 'WebSocket', 'socket.io']
summary: '🐮🐱'
thumbnail: './images/socket.png'
---

# WebSocket과 socket.io

`WebSocket`은 양방향 소통을 위한 프로토콜이다. 여기서 프로토콜은 쉽게 말해서 서로 다른 컴퓨터끼리 소통하기 위한 약속정도로 생각하면 될 것이다.

`socket.io`는 양방향 통신을 하기 위해 웹소켓 기술을 활용하는 라이브러리이다.

그렇게 때문에 socket.io는 WebSocket과 같은 기능을 구현하더라도 약간 느리긴하지만, 대신 많은 편의성을 제공한다.

# WebSocket과 socket.io의 차이점

## WebSocket

- HTML5 웹 표준 기술
- 매우 빠르게 작동하며 통실할 때 아주 적은 데이터를 이용한다.
- 이벤트를 단순히 듣고 보내는 것만 가능하다.

## socket.io

- 표준 기술이 아닌 라이브러리이다.
- 소켓 연결 실패시 fallback을 통해 다른 방식으로 알아서 해당 클라이언트와 연결을 시도한다.
- 방 개념을 이용해 일부 클라이언트에게만 데이터를 전송하는 브로드캐스팅이 가능하다.

# 언제 어떤걸 써야할까?

서버에서 연결된 사용자들을 세밀하게 관리해야 하는 서비스인 경우에는 Broadcasting 기능이 있는 socket.io를 쓰는 것이 유지보수 측면에서 이점이 있다.

but 데이터 전송이 많은 경우에는 빠르고 비용이 적은 표준 WebSocket을 이용하는 것이 이점이 더 많을 것이다.

=> 어떤 서비스를 제공할 것인가에 따라 그때그때 다르게 사용해야한다는 불변의 진리.
