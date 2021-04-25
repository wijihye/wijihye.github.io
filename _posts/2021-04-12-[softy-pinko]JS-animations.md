---
layout: post
title: '[softy-pinko] JS animations'
tags: [study, responsive_web, softy-pinko]
---

#### [softy pinko] JS: animations

Date: Apr 12, 2021

1. JS

   1. home**description**content세 가지는 화면이 load되면 loader과 함께 처리되도록 하였음.
      - setTimeout을 사용하여 한 번만 실행되도록 하였음.
      - 투명도와 translateX를 1500ms동안 실행되도록 함.
   2. IntersectionObserver
      - about section의 img는 opacity와 translateX를 500ms동안 animate함.
      - count section의 h1(숫자)들은 setInterval을 이용하여 특정 시간간격으로 반복되도록 한다. 그 시간마다 숫자를 바꿔주면서 숫자가 증가하는 것 처럼 보이게 함. 원래 html에 있는 숫자만큼 변수가 커지면 setInterval을 중지.

2. 4/12 github commit

   [https://github.com/wijihye/Web-Designs/commit/c03aaaa8e6d60affd3932e32fe8fed36f85dd86f](https://github.com/wijihye/Web-Designs/commit/c03aaaa8e6d60affd3932e32fe8fed36f85dd86f)
