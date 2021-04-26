---
layout: post
title: '[DOM] DOM & CSSOM & RenderTree'
tags: [study, dom, document_object_model, cssom, css_object_model, render_tree]
---

#### [DOM] DOM + CSS => CSSOM (Render Tree)

Date: 2021-04-26

![dom_tree](https://user-images.githubusercontent.com/58647487/116125822-ee03d800-a700-11eb-9c37-184b803db38f.jpg)

---

### Summary

- 모든 Node는 EventTarget을 상속하기때문에 Event를 가질 수 있음.
- Document요소, Element요소, Text요소도 Node를 상속하기 때문에 결과적으로 Event를 가질 수 있음.
- 콘솔 툴을 이용해서 Node를 찾아볼 수 있음.
- CSSOM은 CSS Object Model의 약자로 HTML을 DOM 요소로 변환하고, 이를 CSS 문법과 합친 Render Tree를 말한다.
- <span style="color:tomato">opacity: 0;</span> 이나 <span style="color:tomato">visibility: hidden;</span> 의 경우는 요소가 없어지는 것이 아니기 때문에 Render Tree에 **남아 있으나** <span style="color:tomato">display: none;</span>의 경우처럼 아예 존재하지 않는 경우에는 Render Tree에 **존재하지 않는다.**
