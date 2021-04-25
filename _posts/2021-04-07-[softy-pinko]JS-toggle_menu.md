---
layout: post
title: '[softy-pinko] JS toggle_menu'
tags: [study, responsive_web, softy-pinko]
---

#### [softy pinko] JS: toggle menu

Date: Apr 7, 2021

1. HTML
   - Add script tag.
2. CSS
   - Add a transition for clicked menuicon.
   - If screen size is below 992px, set navbar display none.
   - If screen size is above 992px, set navbar display flex.
3. JS
   - If navbarBtn is clicked, set navbarContents display block.
   - Add addEventListener for window resize event.
     - Remove clicked class
4. 알게된 점
   1. js로 구현 할 때에 예외가 없는지 다시 보기 + commit 시 신중하게 하자. 992px 미만일 때에 menuicon이 'clicked' 된 상태로 화면 크기가 움직이니 navbarContents가 그대로 가는 에러를 강제적?으로 수정했음. 일단 display를 none으로 설정한 후, css에서 해당 element의 display를 flex !important; 로 지정해 992px 이상으로 화면 크기가 커졌을 때는 무조건 flex를 유지하도록 설정을 덮어 줌.
5. 4/7 github commit
   1. [https://github.com/wijihye/Web-Designs/commit/07ac2f7b88f4e2e44be5ebee43a6d35a970701c9](https://github.com/wijihye/Web-Designs/commit/07ac2f7b88f4e2e44be5ebee43a6d35a970701c9)
   2. [https://github.com/wijihye/Web-Designs/commit/47cee65678eeb43670b8fc0e49e7e69a1d33cadd](https://github.com/wijihye/Web-Designs/commit/47cee65678eeb43670b8fc0e49e7e69a1d33cadd)
