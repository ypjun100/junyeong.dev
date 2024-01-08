---
layout: post
categories: [project]
title: SPINMAZE
desc: 원형 미로판을 돌려 미로 안의 공을 빼내는 게임
skills:
  -
    name: Unity
    color: black
    logoColor: white
carousels:
  - images: 
    - image: /imgs/project/spinmaze/spinmaze1.png
    - image: /imgs/project/spinmaze/spinmaze2.png
---

{% include carousel.html height="70" unit="%" duration="15" number="1" showslider="yes" objectfit="contain" %}

## 설명
> 원형 미로판을 회전시켜 미로 안의 공을 빼내는 게임입니다.

## 주요 개발 내용
### 문제없이 회전하는 미로 구현
* 공을 미로판 안에 넣어둔 상태로 미로판을 회전하도록 구현했지만 미로판을 빠르게 회전시킬 때 미로 안의 공이 미로의 벽을 뚫는 버그 발생<br>[참고 영상](https://youtu.be/TKBwmmcy8t8?si=kytQVXCE5qFDLQEJ)
* 관련 내용을 찾던 중 이 프로젝트와 유사한 게임을 개발한 외국 개발자를 발견하여 현재 문제에 대한 참고 영상을 보여주며 해결 방법에 대해 이야기 함
* 이 문제를 해결하기 위해서는 미로판을 그대로 회전하는 것이 아닌 카메라와 중력의 방향을 회전시켜 마치 미로판이 회전하는 듯한 효과를 주도록 구현해야 한다는 것을 깨닫고 이를 구현함