---
layout: post
title: [softy-pinko] JS IntersectionObserver
tags: [study], [responsive_web], [softy-pinko]
---

#### [softy pinko] JS: IntersectionObserver

Date: Apr 15, 2021

1. JS

   - Use IntersectionObserver
     - 앞에서(4/12) 작성한 home_description_content, count를 함수로 축약해 사용함.
       - 그 중에 count는 각 숫자가 HTML에 작성된 범위까지 커지는 속도가 일정하면 나중에 큰 숫자 혼자 counting되므로 각각의 숫자들에 setInterval 간격을 다르게 해 비슷하게 counting이 끝나도록 함. → 함수로 줄였으나 결국 entry4개를 하드코딩 함 .. 어떻게 축약하거나 생산적으로 만들 수 있을까?
     - pricingTable 3개를 home_description_content처럼 animate를 주었음. 스르륵 올라오는 효과를 위하여 각각의 table들에 대해 따로 축약한 함수를 호출함.

2. 4/15 github commit

   [https://github.com/wijihye/Web-Designs/commit/26545ffaea09bf774ed58535f524339f777274ee](https://github.com/wijihye/Web-Designs/commit/26545ffaea09bf774ed58535f524339f777274ee)
