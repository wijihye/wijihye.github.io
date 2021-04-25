---
layout: post
title: '[softy-pinko] Responsive web2'
tags: [study], [responsive_web], [softy-pinko]
---

#### 1. [softy pinko] Responsive web2

Date: Apr 6, 2021

1. CSS

   1. 계속해서 elements들의 width, margin, padding들을 소소하게 바꾸어 가며 최상의 비율을 찾기 위해 노력함..
   2. @media screen and (min-width: 576px, 768px, 992px, 1200px)을 추가하고 각각의 미디어 쿼리 안에 범위 내에서 바뀌어야 하는 element들의 세부 사항을 계속해서 고쳐나감.
   3. count 블럭들에서 특정 px아래로 내려가면 중간의 흰 세개의 원 이미지가 사라지고 예쁘게 정렬될 수 있도록 함.

2. 알게된 점 및 부족한 점

   1. %, rem, em등의 유동적 비율이 사용되어야 하는 곳과 px등의 고정 단위가 언제 사용되어야 할지에 대해 생각해 보게 됨. → 감?만 온 상태

   2. min-width와 max-width에 대해 좀 더 명확히 감을 잡을 수 있었음.

      - min-width는 최소px범위 내에서 적용 한 것들이 가장 우선적으로 적용되므로 min-width로 반응형을 작성한다면 화면 너비(px)을 오름차순으로 작성해야 함.
      - max-width는 반대.

      - 아무리 가장 아래에 적어서 덮어씌워지더라도 위에 쓴 nth-child 가상요소가 적용된 css가 우선적용 됢을 알게 됨.

        ⇒ @media ~ min/max-width에서 nth-child를 다시 작성해 엎어 주어야 함!

3. 4/6 github commit

   [https://github.com/wijihye/Web-Designs/commit/b7195c94b0dd39d9711703b6dc3e12c4e2ab2a03](https://github.com/wijihye/Web-Designs/commit/b7195c94b0dd39d9711703b6dc3e12c4e2ab2a03)
