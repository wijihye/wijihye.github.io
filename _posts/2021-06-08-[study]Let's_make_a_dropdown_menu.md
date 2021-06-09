---
layout: post
title: '[study] dropdown menu 만들기'
tags: [study, web-design]

---

#### web-design - dropdown 형식의 navigation menu 만들기

Date: June 8, 2021

### Git Commit

[https://github.com/wijihye/Web-Designs/commit/a99c66df0b84e6fcd95eb4a45e0311c6d5e3e1c3](https://github.com/wijihye/Web-Designs/commit/a99c66df0b84e6fcd95eb4a45e0311c6d5e3e1c3)

---

### Dropdown 형식의 navigation menu - preview

![dropdownMenu](https://user-images.githubusercontent.com/58647487/121435687-f298ee80-c944-11eb-97f5-00df71afcf1b.gif)

---

### Source

- HTML

  ```html
  <div class="third-wrapper">
        <div class="third-tab about">
          <button class="third-btn about">ABOUT▼</button>
          <div class="third-menus about-div"></div>
        </div>
        <div class="third-tab tech">
          <button class="third-btn tech">TECHNICAL▼</button>
          <div class="third-menus tech-div"></div>
        </div>
        <div class="third-tab prod">
          <button class="third-btn prod">PRODUCT▼</button>
          <div class="third-menus prod-div"></div>
        </div>
      </div>
  ```

- CSS

  ```css
  /* THIRD */
  
  .third-wrapper {
    display: flex;
    position: relative;
    justify-content: left;
    margin: auto;
    margin-top: 100px;
    width: 41em;
    height: 50px;
    background-color: beige;
  }
  
  .third-tab {
    position: relative;
    display: inline-block;
  }
  
  /* div를 한 줄에 정렬하기 위해 display: inline-block으로 설정함. */
  
  .third-tab.about:hover .third-menus.about-div {
    display: block;
  }
  
  .third-tab.tech:hover .third-menus.tech-div {
    display: block;
    left: -79px;
  }
  
  .third-tab.prod:hover .third-menus.prod-div {
    display: block;
    left: -187px;
    /* -79(about btn width)-108(tech btn width) == -187px */
  }
  
  /* 위의 세 가지 tab들이 hover 된 상태일 때 각 drop menu box를 display:block으로
  설정하여 계속 떠있도록 함. 
    결론적으로 -tab div들 안에 menus box들이 있으므로 menubox를 hover 하고 있어도 
  -tab div를 hover하고 있는 것과 같음!!!*/
  
  .third-tab .third-btn {
    box-sizing: content-box;
    border: none;
    background-color: transparent;
    text-decoration: none;
    transition: all 100ms ease-in;
    height: 50px;
    padding: 0 10px;
    margin: 0;
  }
  
  .third-tab:hover .third-btn.about {
    background-color: rgb(248, 135, 150);
  }
  
  .third-tab:hover .third-btn.tech {
    background-color: turquoise;
  }
  
  .third-tab:hover .third-btn.prod {
    background-color: rgb(255, 255, 154);
  }
  
  .third-menus {
    display: none;
    position: absolute;
    box-shadow: 0px 8px 16px 0px rgba(0, 0, 0, 0.2);
    z-index: 1;
    width: 41em;
    height: 200px;
    animation: 350ms fade-in;
    /* 부드러운 효과를 주기 위한 animation */
  }
  
  .third-menus.about-div {
    background-color: pink;
  }
  
  .third-menus.tech-div {
    background-color: skyblue;
  }
  
  .third-menus.prod-div {
    background-color: lemonchiffon;
  }
  
  @keyframes fade-in {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }
  ```

---

### 설명

1. 드롭다운 될 (Hover 효과가 들어갈) 메뉴를 button으로 처리하고, 그 밑의 드롭다운 메뉴들을 div으로 만들어 각 메뉴별로 div로 wrapping함.
2. 메뉴에 Hover될 때 창이 꺼지지 않는 이유는: 결론적으로 메뉴 div는 button과 메뉴 div를 함께 감싼 div 안에 들어있기 때문이다. <span style="color:orange; font-weight:bolder;">Hover 효과는 감싼 div에 줌!! 그래서 메뉴 div도 감싼 div의 Hover 효과 안에 포함된다.</span>

3. 부드러운 효과를 위해 @keyframes를 만들어 fade-in animation을 줌.

---

### 소감

 CSS로 할 수 있는 것들은 정말 많고 나는 그 중 새발의 피만 알고 있는겨.. 진짜 별의 별게 다 CSS로 가능하구나 ㅋㅋㅋㅋㅋ 계속 응용해서 공부하자.

