---
layout: post
title: '[DOM] 스크롤링 이용해 토끼 찾기'
tags: [study, dom, document_object_model]
---

#### [DOM] 스크롤링을 이용한 실습

Date: 2021-04-26

### Preview

![토끼찾기](https://user-images.githubusercontent.com/58647487/116102586-cce3bd00-a6e9-11eb-9560-bb68f40589c1.gif)

---

### Description

- <span style="color:pink;">scrollIntoView</span> 사용.
- carrot, rabbit 이미지는 강의에서 받아옴.
- 눌렀을 때 토끼를 찾는 부드러운 스크롤링: behavior:"smooth", 요소가 중간으로 위치하도록 하는 것: block:'center'

---

### Code

- HTML

  ```html
  <!DOCTYPE html>
  <html lang="en">
    <head>
      <meta charset="UTF-8" />
      <meta http-equiv="X-UA-Compatible" content="IE=edge" />
      <meta name="viewport" content="width=device-width, initial-scale=1.0" />
      <title>Document</title>
      <style>
        body {
          background-color: black;
        }

        .container {
          display: flex;
          flex-flow: column;
          justify-content: center;
          align-items: center;
        }

        .find-btn {
          background-color: rgb(255, 78, 107);
          color: white;
          outline: none;
          font-size: 20px;
          cursor: pointer;
        }

        img {
          width: 150px;
          height: 160px;
        }
      </style>
    </head>
    <body>
      <div class="container">
        <button class="find-btn">Find a Rabbit 🐇</button>
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="rabbit.png" class="rabbit" alt="rabbit" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
        <img src="carrot.png" class="carrot" alt="carrot" />
      </div>
      <script>
        const rabbit = document.querySelector('.rabbit');
        const findBtn = document.querySelector('.find-btn');

        findBtn.addEventListener('click', () => {
          rabbit.scrollIntoView({ behavior: 'smooth', block: 'center' });
        });
      </script>
    </body>
  </html>
  ```

---

### Thinking

- 소스코드가 작아서 그냥 HTML에 CSS, JS 모두 작성함.
- 알고 있었던 scrollIntoView를 실습해 볼 수 있었음.
