---
layout: post
categories: [project]
title: TurtleMQ
desc: WebSocket을 기반한 메시지 브로커
urls:
  -
    type: github
    name: Github
    url: https://github.com/ypjun100/TurtleMQ
skills:
  -
    name: SpringBoot
    color: 6DB33F
    logoColor: white
carousels:
  - images: 
    - image: /imgs/project/turtlemq/architecture.png
---

{% include carousel.html height="30" unit="%" duration="15" number="1" showslider="no" objectfit="cover" %}
_위 이미지에서는 `Lawy`가 TurtleMQ의 클라이언트 역할을 하게 됨_

## 설명
> 작업을 요청하는 `클라이언트`와 작업을 수행 및 계산하는 `Worker`의 역할 분담을 위해 제작한 `WebSocket` 기반 메시지 브로커입니다. RabbitMQ를 모티브로 제작이 되었으며, 마찬가지로 `클라이언트(Producer)`와 `Worker(Consumer)`가 존재합니다.

## 주요 개발 내용
### 클라이언트, Worker 관리
* `클라이언트`가 특정 작업을 요청하는 메시지를 `TurtleMQ`로 전달하면, `TurtleMQ`는 이를 적합한 `Worker`에게 해당 메시지를 전달
* 그리고 작업이 완료되면 반대로 `Worker`에서 `TurtleMQ`를 거쳐 `클라이언트`로 작업 결과를 전달
* 이러한 유기적 통신을 위해 `클라이언트`와 `Worker`는 모두 `TurtleMQ`에서 관리됨
* `TurtleMQ`에서는 이 두 계층의 관리를 위해 아래의 기능들을 제공

### 클라이언트, Worker 등록 및 데이터 통신 과정 수립
* `클라이언트`, `Worker`는 `TurtleMQ`에 등록 메시지를 보내고 승인을 받아야만 정상적으로 데이터를 주고 받을 수 있음
* 두 계층 간 데이터를 주고받기 위한 JSON 객체 구조 정의

### 유휴상태인 Worker에게 메시지 전달
* `TurtleMQ`는 `클라이언트`로 부터 작업 메시지를 받으면, 해당 메시지를 현재 유휴상태인 `Worker`에게 전달함
* `Worker`의 유휴상태 판단을 위해 `Worker`가 작업 메시지를 전달받은 경우 작업중이라고 판단하고, `Worker`가 작업을 완료해 결과값을 전달하면 해당 `Worker`는 유휴상태라 판단

### Worker의 연결이 끊기면 다른 Worker에게 메시지 이관
* 각 `Worker`에서 작업중인 메시지를 서버에서 저장하고 있다가 만약 `Worker`가 작업 도중 연결이 끊기게 된다면 해당 `Worker`가 작업하고 있던 작업 메시지를 그대로 다른 `Worker`에게 이관함
* 만약 연결이 끊긴 `Worker`에서 다시 접속하여 작업 결과를 보낸다면 해당 결과는 무시하도록 설정

### 클라이언트, Worker 간 통신을 WebSocket으로 구현
* `클라이언트`, `Worker`가 `TurtleMQ`와 통신을 할 때 `WebSocket`을 사용