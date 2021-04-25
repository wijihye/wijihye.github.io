---
layout: post
title: [softy-pinko] JS active_nav
tags: [study], [responsive_web], [softy-pinko]
---

#### [softy pinko] JS: active nav

Date: Apr 11, 2021

1. HTML

   - nav의 li > a에 data-link 속성을 이용하여 각 section 태그의 id를 저장함.

2. JS

   - nav menu를 click 시 해당 section으로 이동할 수 있도록 scrollIntoView를 사용했다.
   - nav에서 click 이벤트가 발생하면 해당 a 태그의 dataset을 받아오고 모든 navItem의 'selected' 클래스를 제거한다.
   - 그 후 dataset이 존재하는 구간에 한해서만 'selected' 클래스를 다시 추가하고, 드롭다운 메뉴일 경우에 메뉴를 닫고 이동할 수 있도록 했다.

3. 4/11 github commit

   [https://github.com/wijihye/Web-Designs/commit/db167e457c9ff59e2a9f2f3052d016e518b2c1b6](https://github.com/wijihye/Web-Designs/commit/db167e457c9ff59e2a9f2f3052d016e518b2c1b6)
