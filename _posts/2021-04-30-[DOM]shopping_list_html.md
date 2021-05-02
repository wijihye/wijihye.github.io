---
layout: post
title: '[DOM] Shopping List HTML && CSS'
tags: [study, dom, document_object_model, shopping_list]
---

#### [DOM] 간단한 Shopping List 만들기 (HTML && CSS)

Date: Apr 30, 2021

### GitHub Repository

[GitHub Repo: Browser101](https://github.com/wijihye/Browser101)

### Preview

![shopping-list-HTML](https://user-images.githubusercontent.com/58647487/116776647-7b9a4b80-aaa4-11eb-82aa-9176c4b84f2b.PNG)

### Code

1. HTML

   ```html
   <!DOCTYPE html>
   <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta http-equiv="X-UA-Compatible" content="IE=edge" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>Shopping List</title>
       <link
         rel="stylesheet"
         href="https://use.fontawesome.com/releases/v5.15.3/css/all.css"
         integrity="sha384-SZXxX4whJ79/gErwcOYf+zWLeJdY/qpuqC4cAa9rOGUstPomtqpuNWT9wdPEn2fk"
         crossorigin="anonymous"
       />
       <link rel="stylesheet" href="style.css" />
       <script src="main.js" defer></script>
     </head>
     <body>
       <div class="shopping-list">
         <div class="header">Shopping List</div>
         <div class="listBox"></div>
         <input type="text" class="input" />
         <div class="addBtn">
           <button class="add">+</button>
         </div>
       </div>
     </body>
   </html>
   ```

2. CSS

   ```css
   @import url('https://fonts.googleapis.com/css2?family=Roboto&display=swap');

   :root {
     --color-purple: #c390f3;
     --color-green: #a4e9d2;
   }

   * {
     padding: 0;
     margin: 0;
     font-family: 'Times New Roman', 'Roboto', sans-serif;
   }

   body {
     background-color: hsl(192, 25%, 92%, 0.9);
   }

   .shopping-list {
     margin: 10vh auto;
     width: 50vw;
     height: 75vh;
     background-color: white;
     border-radius: 25px;
     box-shadow: 3px 3px 10px rgba(192, 192, 192, 0.7);
     overflow: hidden;
     min-width: 350px;
     max-width: 450px;
   }

   .header {
     background: linear-gradient(
       15deg,
       var(--color-purple),
       var(--color-green)
     );
     height: 8%;
     text-align: center;
     line-height: 2.5;
     /* font-size의 몇 배*/
     color: white;
     font-size: 1.5em;
     text-shadow: 2px 2px 5px rgb(177, 177, 177);
   }

   .listBox {
     background-color: rgb(248, 248, 248);
     height: 75%;
     font-size: 17px;
   }

   .listBox > ul {
     padding: 10px;
     list-style: none;
   }

   .listBox li {
     margin: 5px 0;
   }

   .listBox span {
     display: inline-block;
     width: 93%;
   }

   .listBox i {
     cursor: pointer;
     padding: 5px;
     transition: color 150ms ease-in;
   }

   .listBox i:hover {
     color: red;
   }

   .input {
     background-color: rgb(255, 255, 255);
     padding: 0 10px;
     width: 96%;
     height: 5%;
     outline: none;
     border: none;
     line-height: 100%;
     font-size: 15px;
   }

   .addBtn {
     background: linear-gradient(15deg, #c390f3, #a4e9d2);
     height: 12%;
     display: flex;
     justify-content: center;
     align-items: center;
   }

   .addBtn .add {
     cursor: pointer;
     width: 60px;
     height: 60px;
     background-color: rgb(161, 161, 161);
     outline: none;
     border: none;
     border-radius: 50%;
     color: white;
     font-size: 50px;
     font-weight: 700;
   }
   ```
