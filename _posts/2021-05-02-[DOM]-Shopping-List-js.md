---
layout: post
title: '[DOM] Shopping List js (complete)'
tags: [study, dom, document_object_model, shopping_list]
---

#### [DOM] Shopping List 완성 -  js 추가

Date: May 2, 2021

### HTML markup

![shopping-list](https://user-images.githubusercontent.com/58647487/116814389-b7600e80-ab93-11eb-9353-1ffc76591d1b.png)

---

### Full Code: JS

```jsx
'use strict';

const LIST_KEY = 'Shopping-List';
const list_ul = document.querySelector('.listBox > ul');
const form = document.querySelector('.input');
const input = document.querySelector('input');
const addBtn = document.querySelector('.add');

let list = [];
// localStorage용 arr
let cnt = 0;

function addElement(itemName) {
  const span = document.createElement('span'); // span 생성
  const i = document.createElement('i'); // i 생성
  const li = document.createElement('li'); // li 생성

  li.id = cnt;
  i.setAttribute('class', 'fas fa-trash-alt delete'); // i에 class 지정
  span.textContent = itemName; // item 이름 넣기

  li.append(span, i); // li에 span, i 넣기. appendChild는 두 개 이상 못 넣음
  list_ul.append(li); // ul에 li 넣기

  list.push({ item: itemName, idx: cnt++ }); // listArr에 넣기

  i.addEventListener('click', delItem);
  setStorage();
}

function setStorage() {
  localStorage.setItem(LIST_KEY, JSON.stringify(list));
}

function addItem(event) {
  const itemName = input.value;
  if (itemName !== '') {
    addElement(itemName);
  }
  input.value = ''; // input의 값 없애기
  input.focus();
  // localStorage의 arr 세팅하기
}

function showItem() {
  const items = JSON.parse(localStorage.getItem(LIST_KEY));
  if (items !== null) {
    items.forEach((item) => {
      addElement(item['item']);
    });
  }
}

function delItem(event) {
  const removeLi = event.target.parentNode; // li 할당
  removeLi.remove(); // li 제거

  const newItems = list.filter((item) => {
    return item.idx !== parseInt(removeLi.id);
  });

  list = newItems;
  setStorage();
}

form.addEventListener('submit', (event) => {
  event.preventDefault();

  addItem(event);
});

addBtn.addEventListener('click', addItem);
showItem();

```

- localStorage 사용해서 F5(refresh) 후에도 list가 사라지지 않도록 함.

---

### 자세한 동작 설명

1. 전역

   ```jsx
   const LIST_KEY = 'Shopping-List';
   const list_ul = document.querySelector('.listBox > ul'); // <li> 생성 후 넣기 위함
   const form = document.querySelector('.input'); // form의 submit 처리 위함
   const input = document.querySelector('input'); // input 태그 값 받아오기 위함
   const addBtn = document.querySelector('.add'); // 추가 버튼 구현 위함
   
   let list = []; // localStorage 덮어쓰기할 임시 arr
   let cnt = 0; // idx 지정하기
   ```

2. input -submit 및 addBtn 동작하게 만들기

   ```jsx
   form.addEventListener('submit', (event) => {
     event.preventDefault(); // submit 발생 시 자동 새로고침 방지
     addItem(event);
   });
   
   addBtn.addEventListener('click', addItem);
   ```

2. addItem 함수

   ```jsx
   function addItem(event) {
     const itemName = input.value;
     if (itemName !== '') {
       addElement(itemName);
     }
     input.value = ''; // input의 값 없애기
     input.focus();
   }
   ```

3. addElement 함수 // document에 element 추가하기

   ```jsx
   function addElement(itemName) {
     const span = document.createElement('span'); // span 생성
     const i = document.createElement('i'); // i 생성
     const li = document.createElement('li'); // li 생성
   
     li.id = cnt;
     i.setAttribute('class', 'fas fa-trash-alt delete'); // i에 class 지정
     span.textContent = itemName; // item 이름 넣기
   
     li.append(span, i); // li에 span, i 넣기. appendChild는 두 개 이상 못 넣음
     list_ul.append(li); // ul에 li 넣기
   
     list.push({ item: itemName, idx: cnt++ }); // listArr에 넣기
   
     i.addEventListener('click', delItem);
     setStorage();
   }
   ```

   - span, i, li를 만들어서 속성을 지정해준다.

   - li에는 id를 cnt값으로 넣어서 localStorage와 동시에 삭제가 용이하도록 설정한다.

   - list라는 빈 배열에 item 이름과 idx 를 함께 지정하여 obj형태로 push(뒤로 쌓기)한다.  

     <span style="color:blue">=== 초기에 localStorage에 있는 값을 무조건 다 훑기 때문에 전역에서는 빈 list였으나 이 함수가 실행되고 난 후의 list는 무조건 localStorage의 값을 다 갖고 있다. 그래서 push하면 값이 계속 쌓이게 된다!</span>

   - i에 click 이벤트 핸들러를 등록한다. **delItem** 함수를 할당한 뒤 **setStorage**(바뀐 list를 localStorage에 덮어씌우기)를 호출한다.

4. setStorage 함수

   ```jsx
   function setStorage() {
     localStorage.setItem(LIST_KEY, JSON.stringify(list));
   }
   ```

   - localStorage에는 obj 형식을 저장할 수 없기 때문에 (string 만 가능) JSON.stringify를 이용하여 string 화 시켜준다.

5. showItem 함수

   ```jsx
   function showItem() {
     const items = JSON.parse(localStorage.getItem(LIST_KEY));
     if (items !== null) {
       items.forEach((item) => {
         addElement(item['item']);
       });
     }
   }
   ```

   - localStorage에 넣은 obj 배열을 JSON.parse를 통해 변환하여 받아온다.
   - items를 하나씩 돌면서 key가 'item' 인 value들을 가져와 **addElement**에 전달한다.
   - <span style="color: blue">**addElement**에서 list에 push해주는 역할을 하기 때문에 list는 항상 localStorage의 온전한 형태를 갖고 있다.</span>
   - 초기에 한 번 무조건 실행해준다. document에 element 추가하여 사용자에게 보여야 하기 때문.

6. delItem 함수

   ```jsx
   function delItem(event) {
     const removeLi = event.target.parentNode; // li 할당
     removeLi.remove(); // li 제거
   
     const newItems = list.filter((item) => {
       return item.idx !== parseInt(removeLi.id);
     });
   
     list = newItems;
     setStorage();
   }
   ```

   - removeLi 변수에는 지금 event로 전달된 <i>의 부모 (<li>)를 할당한다. (parentNode 사용)

   - remove API를 이용하여 해당 <li>를 삭제한다. -> document에서 사라짐!

   - 현재 list에 있는 obj들의 각 idx와 지금 삭제된 <li>에 할당되어있던 id들을 비교하여 같지 않은 것들만 담는다.

     ```text
     ex)
     나는 현재 id값이 2인 <li>를 삭제하였다. 이를 localStorage에도 적용시키기 위해 filter API를 사용한다.
     
     localStorage에는 idx값이 2인 obj가 들어 있는데, 이를 포함한 모든 obj들의 idx를 비교하면 이미 제거한 id와 모두 비교하면 결국에 newItems에는 삭제된 id: 2 (idx: 2) 빼고 모든 obj들이 담기게 된다. 
     
     이를 list에 덮어씌우고 localStorage에 저장한다.
     ```

---

### Thinking

1. localStorage를 사용하는 것은 예전에 momentum clone 에서도 했었는데, 좀 오래돼서 기억이 안났다.
2. 그래서 코드를 참고했다. (toDo.js) notion: [momentum clone](https://www.notion.so/Momentum-Chrome-app-clone-codings-7d69cb2600404c448d1df771899909a4)
3. localStorage를 사용하기 위해 빈 list를 사용하여 이 함수 저 함수에서 돌아가면서 list의 값을 변경하고 덮어씌우고 하는 방식이 갑자기 이해가 안돼서 애를 먹었는데, 이렇게 다시 정리하면서 써보니까 이해가 된다 ㅜㅜ 다행..