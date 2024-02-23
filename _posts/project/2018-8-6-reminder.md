---
layout: post
categories: [project]
title: REMINDER
desc: 버릇 교정을 도와주는 머신러닝 기반 IOT 디바이스
urls:
  -
    type: youtube
    name: 프로젝트 소개 영상
    url: https://www.youtube.com/watch?v=vB_ea0pDKl4
skills:
  -
    name: Tensorflow
    color: FF6F00
    logoColor: white
  -
    name: Arduino
    color: 00878F
    logoColor: white
people: [머신러닝 엔지니어 1명, 아두이노 개발 2명, 앱 개발 1명]
carousels:
  - images: 
    - image: /imgs/project/reminder/reminder1.jpg
    - image: /imgs/project/reminder/reminder2.jpg
---

{% include carousel.html height="70" unit="%" duration="15" number="1" showslider="yes" objectfit="contain" %}

## 설명
> 손톱을 물어뜯거나 어딘가를 긁는 버릇을 교정할 수 있도록 손목에 착용하는 아두이노 디바이스를 이용해 버릇을 행하면 디바이스 내의 진동모터를 통해 진동을 줍니다. 그리고 앱 내에서 오늘 버릇을 몇 번 했는지 모니터링할 수 있는 기능을 제공합니다.

## 주요 담당 내용
### 리더
* 팀원들에게 편한 분위기를 제공하여 자유로운 아이디어를 낼 수 있는 환경 구축
* 팀원이 겪고있는 이슈사항에 대해 팀원 혼자 해결하기 보다 모두가 같이 모여 이야기하며 해결할 수 있도록 함

### 머신러닝 엔지니어 및 아두이노 코딩
* `아두이노`에서 도출된 `가속도 센서값`을 이용해 `딥러닝 모델`을 사용하여 버릇 탐지

## 주요 개발 내용
### 아두이노 디바이스 코딩
* 사용자가 손을 움직일 때 들어오는 `가속도 센서값`을 저장했다가 움직임이 끝났을 때 `블루투스` 통신을 이용해 휴대폰으로 전송되도록 구현
* 가속도 센서값을 보정하기 위한 `보정 필터` 사용

### 버릇 탐지 머신러닝 모델 구현
* 손톱 물어뜯기, 옆 머리 긁기, 뒷 목 긁기 버릇에 대해서 아두이노 기기를 손목에 착용한 상태로 세 가지의 버릇을 행하여 데이터셋 구축
* 다양한 데이터셋 구성을 위해서 같은 버릇을 다양한 자세(서서, 누워서, 옆으로 누워서 등)에서 진행
* `CNN 모델`을 구성하여 모델 학습 진행 후 안드로이드 앱에 탑재