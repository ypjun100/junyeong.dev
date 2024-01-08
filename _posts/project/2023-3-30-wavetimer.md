---
layout: post
categories: [project]
title: wavetimer
desc: 파동 효과를 활용한 웹 Pomodoro 타이머
urls:
  -
    type: website
    name: wavetimer
    url: https://wavetimer.junyeong.dev
  -
    type: website
    name: 프로젝트 회고
    url: https://blog.junyeong.dev/posts/wavetimer-%ED%94%84%EB%A1%9C%EC%A0%9D%ED%8A%B8-%ED%9A%8C%EA%B3%A0/
  -
    type: github
    name: Github
    url: https://github.com/ypjun100/wavetimer-front
skills:
  -
    name: React
    color: 61DAFB
    logoColor: black
carousels:
  - images: 
    - image: /imgs/project/wavetimer/wavetimer.gif
---

{% include carousel.html height="70" unit="%" duration="15" number="1" showslider="no" objectfit="cover" %}

## 설명
> 흐르는 액체의 양으로 타이머의 시간이 얼마나 남았는지를 확인할 수 있는 Pomodoro 타이머입니다. 액체의 파동 효과를 구현하기 위해 파동 방정식을 활용하여 구현하였습니다.

## 주요 개발 내용
### Pixi.js를 활용한 배경의 파동 효과 구현
* 파동방정식을 사용하여 사용자의 이벤트가 발생하였을 때 적절한 파동 효과가 나타나도록 구현
* 기본적으로 제공하는 `Canvas`로는 배경의 파동을 그릴 때 브라우저 별로 똑같은 블렌딩 모드를 구현하기 어려웠기 때문에 `Canvas`가 아닌 `Pixi.js` 그래픽 엔진을 사용하여 배경 구현

### 애니메이션을 차례대로 실행할 수 있도록 애니메이션 큐 구현
* 동시에 애니메이션 요청이 들어온 경우 요청 두 개가 동시에 시작되는 문제가 발생
* 따라서 하나의 애니메이션이 종료된 후 그 다음 애니메이션이 실행될 수 있도록 `애니메이션 큐` 구현

### 라이트 / 다크 테마 지원
* 사용자의 편의성을 위한 `라이트 / 다크 모드` 지원