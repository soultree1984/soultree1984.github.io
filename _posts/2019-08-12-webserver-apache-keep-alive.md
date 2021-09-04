---
title: 'Keep Alive 에 대해 설명해보세요.'
author: soultree1984
date: 2019-08-12 10:22
categories: [Interview]
tags: [Http Protocol, Web Server, Apache ]
---

> Keep Alive 에 대해 설명 해줄 수 있나요?

## "아 그거 Apache 설정에서 봤는데 정확히는 잘 모르겠습니다."

서버에 Apache 설치는 몇번 해봤었는데, 그때 httpd.conf 파일에서 봤던 옵션이었다.
Keep Alive 설정을 이야기 하기 전에 HTTP 얘기를 먼저 해야겠다.

> HTTP는 무상태(stateless), 비연결성(connectionless)의 특징을 가진다.

### 무상태(stateless)

 데이터를 주고 받기 위한 각각의 데이터 요청이 서로 독립적으로 관리가 된다는 말로,
 이전의 데이터 요청과 다음의 데이터 요청은 서로 관련이 없다는 말이다.

### 비연결성(connectionless)

이 비연결성이 Keep Alive 와 관련이 있는 특징인데, HTTP는 연결을 매번 끊고 새로 생성하는 구조로
설계되어 Network 비용 측면에서 많은 비용을 소비하는 구조 이다. 이에 대한 해결책으로 Keep Alive 라는
기능을 HTTP 1.1 부터 지원 했다. Keep Alive는 max / timeout 2개의 속성이 있는데<br/>

timeout 하나의 연결이 유지되는 시간(초)이고 max 는 하나의 연결이 끝나기 전까지 요청 할 수 있는 최대 요청 수이다.
**Keep-Alive: max=5, timeout=120** 처럼 설정을 하면 한번 요청된 연결은 120초 동안 유지 되고, 연결이 종료되기 전까지 최대 5번의 요청까지 허용한다는 이야기다.
timeout 시간을 초과하거나, max 값을 초과하면 연결은 끊어지고 새로운 연결이 생성된다.

요청(request)의 응답(response) 데이터는 아래처럼 내려온다.

e.g.)
````
~$ curl -I https://www.domain.com/file.html
HTTP/1.1 200 OK
Connection: Keep-Alive
Content-Type: text/html; charset=UTF-8
Date: Thu, 15 Jan 2015 16:45:29 GMT
Content-Length: 1845
Keep-Alive: timeout=5, max=120
Server: Apache/2.4.9 (Unix) PHP/5.6.2
````

### 이번글은 여기까지만 알아보자.
