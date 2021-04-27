---
layout: post
title: '[DOM] textContext vs innerText vs innerHTML'
tags: [study, dom, document_object_model, textContext, innerText, innerHTML]
---

#### [DOM] textContext, innerText, innerHTML 비교하기

Date: Apr 27, 2021

![textContext-innerText-innerHTML](https://user-images.githubusercontent.com/58647487/116291695-d9dadc00-a7cf-11eb-92fa-acdb06076382.jpg)

#### XSS Attack?

- XSS: Cross-Site Scripting
- XSS is a term used to describe a class of attacks that allow an attacker to inject client-side scripts _through_ the website into the browsers of other users.
- [XSS -mdn](https://developer.mozilla.org/en-US/docs/Learn/Server-side/First_steps/Website_security)

### Thinking

- 단순한 문자열을 변경할 경우에는 거의 다 textContext를 쓰면 될 것 같음.

- innerHTML은 HTML 구문분석을 하기 때문에 여러 번 바뀌는 효과에는 사용하기에 비싸다.

  => createElement, appendChild, setAttribute, removeChild 등의 Element를 사용하는 방식이 더 나을 수도 있음.

- <span style="color: red">어떻게 하면 효율 좋은 웹페이지를 구현할까? 라는 질문에 대해서는 정말 많은 고민과 앎이 있어야 할 것 같다!</span>
