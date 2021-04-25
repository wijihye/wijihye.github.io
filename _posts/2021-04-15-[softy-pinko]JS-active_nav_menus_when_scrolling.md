---
layout: post
title: [softy-pinko] JS active nav menus
tags: [study], [responsive_web], [softy-pinko]
---

#### [softy pinko] JS: active nav menus when scrolling

Date: Apr 15, 2021

1. JS

   - window에 'wheel' 이벤트가 전달되었을 때 nav menu들에 해당하는 section이 화면에 보이는 중이면 그에 맞는 navbar menu에 'selected' class를 추가함.

     - !entry.isIntersecting일 때 section들의 id를 모아놓은 배열에서 해당 entry.target의 id를 불러와 배열의 인덱스를 찾음.

     - entry.boundingClientRect.y는 만약 해당 element가 scroll되어 위로 올라가면 -(음수)값을 갖기 때문에 지금 현재 위로 올라갔는지, 아래에 있는지를 알 수 있다.

       ⇒ entry.boundingClientRect.y를 이용하여 scroll 방향을 알고 다음 section의 idx를 예상하는 역할을 함! ★이해하기★

     - 이 조건에 들어갔을 때 배열상의 idx를 이용하여 selectedMenuIdx, 즉 현재 선택된 nav menu 인덱스를 계산한다.

     - 'wheel' 이벤트가 발생했을 때 스크롤이 가장 위에 있거나 아래에 있으면 선택되는 selectedMenuIdx를 임의로 지정한다.

       - 맨 아래에 있는 것을 계산하기 위해 window.innerHeight와 window.scrollY를 더한 것을 반올림한 것과 document.body.clientHeight가 같으면(문서 전체 길이: 고정=== 현재 스크롤 길이: 바뀜 + 화면 너비: 고정)
       - selectedMenuIdx가 지정되면 함수를 호출하여 'selected' class를 제거하거나 추가한다. 추가 및 제거를 용이하게 하기 위하여 현재 'selected'가 있는 element를 전역변수에 함께 저장한다.

2. 4/15 github commit

   [https://github.com/wijihye/Web-Designs/commit/10600c9ab4b5596db8558afc17885f5af611fb5c](https://github.com/wijihye/Web-Designs/commit/10600c9ab4b5596db8558afc17885f5af611fb5c)
