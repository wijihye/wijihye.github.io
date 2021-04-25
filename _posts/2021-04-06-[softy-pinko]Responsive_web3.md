---
layout: post
title: '[softy-pinko] Responsive web3'
tags: [study], [responsive_web], [softy-pinko]
---

#### [softy pinko] Responsive web3

Date: Apr 6, 2021

1. HTML

   - 화면 너비 특정 px 아래에서 navbar가 버튼을 이용해 드롭다운 형태로 보여질 수 있게끔 버튼요소를 CSS로 꾸며서 추가함.
     - input type="checkbox" 요소의 checked 속성을 이용한다!! 매우 신박함.
     - label의 for 속성과 checkbox의 name 속성을 같게끔 코딩해주면 label을 클릭해도 checkbox가 동작하는 형태가 된다.
     - label태그 안에 span 세 개를 넣고 span을 css로 꾸민다. 이때 checkbox의 display는 none으로 한다.
     - checkbox의 외관은 보이지 않지만 label의 for에 작성한 것으로 인해 checked 속성을 사용할 수 있다. 따라서 checked되었을 때 세 span 중 맨 위+맨 아래 span이 회전하며 X 모양을 만들고, 중간 위치의 span을 opacity: 0;으로 처리하여 자연스러운 transition을 준다.

2. CSS

   - navbar의 logo img 및 nav\_\_item들의 padding, margin, width 등을 자연스럽게 조절함.

3. 알게된 점

   1. checkbox/radio와 label의 연관성 및 꾸밈 방법

4. 4/6 github commit

   [https://github.com/wijihye/Web-Designs/commit/3bdf2f217bf440cc55713067e04169d2999c8cac](https://github.com/wijihye/Web-Designs/commit/3bdf2f217bf440cc55713067e04169d2999c8cac)
