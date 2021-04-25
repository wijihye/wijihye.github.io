---
layout: post
title: '[study] mini-shopping-mall'
tags: [study, simple-game]
---

#### mini-shopping-mall

Date: Mar 8, 2021

Show list of three types of clothes or three colors of clothes

##### Photos

1. show all list

![main](https://user-images.githubusercontent.com/58647487/115872980-622e4980-a47d-11eb-8897-c87cd82ca553.png)

2. filtered by type

![filtered_by_type1](https://user-images.githubusercontent.com/58647487/115873219-a28dc780-a47d-11eb-8cdb-33aea15a6aa3.png)

3. filtered by color

![filtered_by_color1](https://user-images.githubusercontent.com/58647487/115873281-b6392e00-a47d-11eb-83b2-1eda52e4435c.png)

##### Codes

#### HTML

```html
<!DOCTYPE html>
	<html lang="en">
        <head>
            <meta charset="UTF-8" />
            <meta http-equiv="X-UA-Compatible" content="IE=edge" />
            <meta name="viewport" content="width=device-width, initial-scale=1.0" />
            <script defer src="main.js"></script>
            <link rel="stylesheet" href="style.css" />
        </head>
        <body>
            <!-- Logo -->
            <img src="img/logo.png" alt="logo image" class="logo" />
            <!-- Buttons-->
            <div class="buttons">
                <button class="btn">
                    <img src="img/blue_t.png" alt="tshirt" class="imgBtn" data-key="type" data-value="tshirt"/>
               </button>
                <button class="btn">
                    <img src="img/blue_p.png"alt="pants"class="imgBtn"data-key="type"data-value="pants"/>
                </button>
                <button class="btn">
                    <img src="img/blue_s.png"alt="skirt"class="imgBtn"data-key="type"
    data-value="skirt"/>
                </button>
                <button class-"btn colorBtn blue" data-key="color" data-value="blue">
                    Blue
                </button>
                <button class="btn colorBtn yellow" data-key="color" data-value="yellow">
                    Yellow
                </button>
                <button class="btn colorBtn pink" data-key="color" data-value="pink">
                    Pink
                </button>
            </div>
            <!-- Items -->
            <ul class="items">
            </ul>
        </body>
    </html>
```

#### CSS

```css
@import '/reset.css';

:root {
  /* color */
  --color-black: #3f454d;
  --color-white: #ffffff;
  --color-blue: #3b88c3;
  --color-yellow: #fbbe28;
  --color-pink: #fd7f84;
  --color-light-grey: #dfdfdf;

  /* size */
  --base-space: 8px;
  --size-button: 60px;
  --font-size: 18px;
  --size-border: 4px;
  --size-thumbnail: 50px;

  /* animation */
  --animation-duration: 300ms;
}

body {
  height: 100vh;
  background-color: var(--color-black);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.logo {
  cursor: pointer;
  transition: transform var(--animation-duration) ease;
}

.btn {
  background-color: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  transition: transform var(--animation-duration) ease;
  margin-right: var(--base-space);
}

.buttons {
  display: flex;
  align-items: center;
}

.btn:hover,
.logo:hover {
  transform: scale(1.1);
}

.imgBtn {
  width: var(--size-button);
  height: var(--size-button);
}

.colorBtn {
  font-size: var(--font-size);
  padding: calc(var(--base-space) * 2);
  border-radius: var(--size-border);
}

.blue {
  background-color: var(--color-blue);
}

.yellow {
  background-color: var(--color-yellow);
}

.pink {
  background-color: var(--color-pink);
}

.items {
  width: 60%;
  height: 60%;
  overflow-y: scroll;
  list-style: none;
  padding: 0;
}

.items::-webkit-scrollbar {
  display: none;
}

.item {
  background-color: var(--color-white);
  display: flex;
  align-items: center;
  padding: var(--base-space);
  margin-bottom: var(--base-space);
  border-radius: var(--size-border);
}

.item__thumbnail {
  width: var(--size-thumbnail);
  height: var(--size-thumbnail);
}

.item__description {
  margin-left: var(--base-space);
  font-size: var(--font-size);
}
```

### JS - my.ver

```jsx
'use strict';

const logo = document.querySelector('.logo');
const btns = document.querySelector('.buttons');

// Fetch the items from the JSON file
function loadItems() {
  return (
    fetch('data/data.json')
      // 1. fetch로 불러온 결과가 성공적이면
      .then((response) => response.json())
      // 2. 결과를 json으로 반환하고
      .then((json) => json.items)
    // 3. json 안의 items를 가져온다.
  );
  // 결국 반환값은 Promise
}

// Update the list with the given items
function displayItems(items) {
  const container = document.querySelector('.items');
  container.innerHTML = items.map((item) => createHTMLString(item)).join('');
}

// Create li tag that is in the container
function createHTMLString(item) {
  return `
  <li class="item">
    <img src="${item.image}" alt="${item.type}" class="item__thumbnail" />
    <span class="item__description">${item.gender}, ${item.size}</span>
  </li>
  `;
}

// Reload this page
function pageReload() {
  location.reload();
}

// Filter these itmes that fit the conditions
function filtering(e) {
  const typeFilter = e.target.alt;
  const colorFilter = e.target.classList[2];
  const container = document.querySelector('.items');
  // type분류 버튼을 눌렀는지 color분류 버튼을 눌렀는지 알기 위해 일단 두개 다 받기
  // + ul 안의 html 작성 위해 container 받아오기

  loadItems().then((items) => {
    // item을 받아오는 데 성공하면 - .
    if (colorFilter) {
      // 만약 color 분류 버튼을 눌렀으면
      const itemList = items.filter((item) => colorFilter === item.color);
      // callback조건이 참인 요소만 뽑아 배열로 생성해주는 filter함수 사용1
      container.innerHTML = itemList
        .map((item) => createHTMLString(item))
        .join('');
      // container의 innerHTML 변경1
    } else if (typeFilter) {
      // 만약 type 분류 버튼을 눌렀으면
      const itemList = items.filter((item) => typeFilter === item.type);
      // .. filter 함수 사용2
      container.innerHTML = itemList
        .map((item) => createHTMLString(item))
        .join('');
      // container의 innerHTML 변경2
    }
    // 뭔가 if 조건 없이 그냥 두 개를 다 적으면 조금이라도 손실?이 있을까봐
    // 나눠 적었는데 data양이 작아서 그다지 의미 없는 듯 ...?
  });
}

function setEventListeners(items) {
  // eventListner 관리
  logo.addEventListener('click', pageReload);
  // logo 버튼을 눌렀을 때에는 page가 reload 되도록 함
  btns.addEventListener('click', filtering);
  // btn들(6가지)을 모두 가져와 click 이벤트가 발생했을 때 filtering 함수를 실행함.
}

// main
loadItems()
  .then((items) => {
    displayItems(items);
    setEventListeners(items);
  })
  .catch(console.log);
```

#### JS - teacher.ver

```jsx
'use strict';

const logo = document.querySelector('.logo');
const btns = document.querySelector('.buttons');

// Fetch the items from the JSON file
function loadItems() {
  return (
    fetch('data/data.json')
      // 1. fetch로 불러온 결과가 성공적이면
      .then((response) => response.json())
      // 2. 결과를 json으로 반환하고
      .then((json) => json.items)
    // 3. json 안의 items를 가져온다.
  );
  // 결국 반환값은 Promise
}

// Update the list with the given items
function displayItems(items) {
  const container = document.querySelector('.items');
  container.innerHTML = items.map((item) => createHTMLString(item)).join('');
}

// Create li tag that is in the container
function createHTMLString(item) {
  return `
  <li class="item">
    <img src="${item.image}" alt="${item.type}" class="item__thumbnail" />
    <span class="item__description">${item.gender}, ${item.size}</span>
  </li>
  `;
}

function onButtonClick(event, items) {
  const dataset = event.target.dataset;
  const key = dataset.key;
  const value = dataset.value;

  if(key == null || value == null) return;

  displayItems(items.filter(item => item[key] === value))
}

function setEventListeners(items) {
  // eventListner 관리: 다른점★
  logo.addEventListener('click', e => displayItems(items);
  btns.addEventListner('click', event => onButtonClick(event, items));
}

// main
loadItems()
  .then((items) => {
    displayItems(items);
    setEventListeners(items);
  })
  .catch(console.log);
```

#### Review

Two codes are different on the way of filtering.

In my case, First, I take target's attribute(img: alt, button: class) and element that is ul tag in the function. And then, load the items using a function named loadItems. But it has problem like repeated loading and filtering items .

In teacher's case, using exist functions and two of html datasets. Her code is shorter than me! But it has the same problem of mine. (repeated filtering items)

So, I change the way of filtering. That is using css display:none!

##### Using CSS code(js)

```jsx
'use strict';

const logo = document.querySelector('.logo');
const btns = document.querySelector('.buttons');
const container = document.querySelector('.items');

// Fetch the items from the JSON file
function loadItems() {
  return (
    fetch('data/data.json')
      // 1. fetch로 불러온 결과가 성공적이면
      .then((response) => response.json())
      // 2. 결과를 json으로 반환하고
      .then((json) => json.items)
    // 3. json 안의 items를 가져온다.
  );
  // 결국 반환값은 Promise
}

// Create li elements which is in ul
function createElement(item) {
  const li = document.createElement('li');
  const img = document.createElement('img');
  const span = document.createElement('span');

  // img.setAttribute('class', 'item__thumbnail'); or
  img.classList.add('item__thumbnail');
	// img.setAttribute('src', item.image); or
	img.src = item.image;
  // img.setAttribute('alt', item.type); or
  img.alt = item.type;


  // span.setAttribute('class', 'item__description'); or
  span.classList.add('item__description');
  span.innerHTML = `${item.gender}, ${item.size}`;

  // li.setAttribute('class', 'item'); or
  li.classList.add('item');
	// li.setAttribute('data-type', item.type); or
	li.dataset.type = item.type;
  // li.setAttribute('data-color', item.color); or
	li.dataset.color = item.color;

  li.append(img);
  li.append(span);

  return li;
}

// Filter what is visible elements
function visibleItems(event, itemElements) {
  const dataset = event.target.dataset;
  const key = dataset.key;
  const value = dataset.value;

  if (key == null || value == null) return;

  updateItems(itemElements, key, value);
}

// Update items that should be seen
function updateItems(itemElements, key, value) {
  itemElements.forEach((element) => {
    if (element.dataset[key] === value) element.classList.remove('invisible');
    else element.classList.add('invisible');
  });
}

// main
loadItems()
  .then((items) => {
    const itemElements = items.map(createElement);
    container.append(...itemElements);
		// ...을 붙이면 DOMString, Node List 등을 Elements로 바꿔준다.
    btn.addEventListener('click', event => visibleItems(event, itemElements);
  })
  .catch(console.log);
```

##### Something new to know

- append(...node): Change DOMString or Node to HTML Element

- how to filter items as many ways
