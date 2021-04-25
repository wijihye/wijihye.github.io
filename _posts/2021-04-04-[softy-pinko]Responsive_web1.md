---
layout: post
title: '[softy-pinko] Responsive web1'
tags: [study, responsive_web, softy-pinko]
---

#### [softy pinko] Responsive web1

Date: Apr 4, 2021

1. HTML

   - max-width를 지정하기 위해 몇몇 section 아래에 div.container를 삽입함

2. CSS
   - pricing table이 화면 너비 768px 이하일 때 100%로 화면을 가득 채울 수 있게 함.
   - blog entries가 flex-wrap: wrap;이 되도록 하고, margin 및 사진 크기를 조정하여 재배치함.
   - testimonials가 flex-wrap: wrap;이 되도록 함.
   - about의 description들이 justify-content: space-between → center이 되도록 해 wrap 되었을 때 자동 중앙 정렬이 되도록 함.
   - work process의 justify-content: space-between → center 및 wrap 지정.
   - 그 외의 자잘한 margin, padding, width를 지정하였음
   - wrap 되었을 때 section의 height가 자동으로 같이 늘어나게 하기 위해 section의 height를 모두 제거함!!
3. 알게된 점

   - wrap을 처음부터 지정해 놓으면 나중에 responsive web을 만들 때 한결 편안하게 만들 수 있을 것 같다.
   - section 및 div의 height를 지정해 놓으면 wrap등으로 인해 해당 box의 높이가 변경되었을 때 유동적으로 변경할 수 없음.

   반응형으로 만들 것을 대략 생각해서 짠 후 특정 px(화면 너비)에 대응하도록 조금씩 수정해보자.

4. 4/4 github commit

   [https://github.com/wijihye/Web-Designs/commit/ddb81d59d543a60f02db0b1bfcb120d966870fb2](https://github.com/wijihye/Web-Designs/commit/ddb81d59d543a60f02db0b1bfcb120d966870fb2)
