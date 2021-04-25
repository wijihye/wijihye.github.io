---
layout: post
title: '[softy-pinko] CSS change wrap style'
tags: [study], [responsive_web], [softy-pinko]
---

#### [softy pinko] CSS: change wrap style

Date: Apr 15, 2021

1. HTML

   - pricing-table을 감싸는 div를 추가함 (각각, 총 3개)

2. CSS

   1. card-cover과 마찬가지로 화면 너비(문서 너비)에 따라 flex 설정을 따로 준다.
   2. flex: 0 0 ~%;
      - flex: [flex-grow: 커질 때 비율] [flex-shrink: 축소될 때 비율] [flex-basis: flex 축에 따른 아이템의 기본 크기]
      - 를 지정하여 wrap 되었을 때 중앙정렬이 아닌 왼쪽부터 차례로 box들이 정렬될 수 있게 함.
      - 주의!! justify-content: center; margin-left, margin-right를 auto로 지정하면 자동으로 아래에 wrap된 contents가 중앙정렬된다.

3. 알게된 점

   - 새로이 wrap을 정렬하는 방식을 알게 되었다.. 또한 margin의 값을 -로 주어 안의 요소들을 조금 더 넓게 보이도록 할 수 있다는 것도 알게 되었다.!!

4. 4/15 github commit

   [https://github.com/wijihye/Web-Designs/commit/46be50629eaa0a419f29ea947e54776d0c18ca7b](https://github.com/wijihye/Web-Designs/commit/46be50629eaa0a419f29ea947e54776d0c18ca7b)
