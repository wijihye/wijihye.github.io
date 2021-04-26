---
layout: post
title: '[DOM] 마우스 좌표 찾기'
tags: [study, dom, document_object_model]
---

#### [DOM] 마우스 좌표찾기 실습

Date: 2021-04-26

### Preview

![좌표찾아007](https://user-images.githubusercontent.com/58647487/116045447-077b3480-a6ad-11eb-9b3e-b7487704bfba.gif)<br>

---

### Description

- window의 <span style="color:pink;">mousemove</span> 이벤트를 사용함.
- target이미지는 강의에서 받아옴
- 실시간으로 위치가 변경되는 것은 JS에서 CSS: transform을 이용하여 구현함.
- 맨 처음 화면에서는 안보이다가 마우스가 window 위에 올라가는 순간부터 동작하도록 display를 none->block으로 변경함.

---

### Code

- CSS

  ```css
  body {
    background-color: black;
    margin: 0;
    position: relative;
    color: white;
    font-size: 30px;
  }

  .x,
  .y,
  .desc,
  .target {
    display: none;
  }

  .desc {
    position: absolute;
    top: -60px;
    left: 30px;
  }

  .target {
    position: absolute;
    top: -60px;
    left: -60px;
    z-index: 100;
  }

  .y {
    width: 100%;
    height: 1px;
    margin-top: 1px;
    background-color: white;
  }

  .x {
    width: 1px;
    height: 99.5vh;
    background-color: white;
  }
  ```

- JS

  ```jsx
  const y = document.querySelector('.y');
  const x = document.querySelector('.x');
  const targetImg = document.querySelector('.target');
  const description = document.querySelector('.desc');

  window.addEventListener('mousemove', (event) => {
    const mouseX = event.clientX;
    const mouseY = event.clientY;

    // change state of display
    description.style.display = 'block';
    targetImg.style.display = 'block';
    y.style.display = 'block';
    x.style.display = 'block';

    description.innerText = `${mouseX}, ${mouseY}`;
    description.style.transform = `translate(${mouseX}px, ${mouseY}px)`;

    targetImg.style.transform = `translate(${mouseX}px, ${mouseY}px)`;

    x.style.transform = `translateX(${mouseX}px)`;
    y.style.transform = `translateY(${mouseY}px)`;
  });
  ```

- HTML

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
      <script src="main.js" defer></script>
    </head>
    <body>
      <img src="target.png" alt="target" class="target" />
      <div class="desc"></div>
      <div class="y"></div>
      <div class="x"></div>
    </body>
  </html>
  ```

---

### Teacher's solution

1.  div들을 absolute로 주고 left와 top을 이용하여 위치를 계속 변경함.

    ```jsx
    ...
    vertical.style.left = `${x}px`;
    horizontal.style.top = `${y}px`;

    target.style.left = `${x}px`;
    target.style.top = `${y}px`;
    // tag도 마찬가지로 진행.
    ...
    ```

2.  innerText 대신 innerHTML 사용

    - <span style="background-color:yellow; color:black;">innerText</span>는 IE에서 이전버전에 쓰였기 때문에 더 이상 표준에 맞지 않다. 이제 사용 X

    - <span style="background-color:yellow; color:black;">innerHTML</span>은 HTML 태그를 포함한 string을 설정할 수 있음. => HTML요소도 추가 가능하다!

      ```html
      Teacher's comment: 보안상의 문제는 innerHTML에서 XSS(Cross Site Scripting)
      attack 보안 문제가 있는데 이는 사용자에게 입력을 받아온 데이터를
      innerHTML로 설정할 경우 문제가 되어요. 즉 임의의 사용자가 input을 통해서
      script를 포함한 텍스트를 입력해서 공격을 할 수 있죠 :)
      ```

---

### Thinking

- x와 y를 매번 event.clientX, event.clientY가 아닌 변수로 할당한 점은 선생님과 같다ㅋㅎㅋㅎ
- 다른사람 한 것을 보니까 canvas로 하던데 생각보다 canvas의 활용범위가 무궁무진한듯!
- 이 정도 과제는 정말 혼자 가능해졌다. 좀 더 노력하자!
- <span style="color:darkred">innerText가 아닌 innerHTML 사용하기</span>
