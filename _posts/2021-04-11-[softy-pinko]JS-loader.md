---
layout: post
title: '[softy-pinko] JS loader'
tags: [study, responsive_web, softy-pinko]
---

#### [softy pinko] JS: loader

Date: Apr 11, 2021

1. HTML

   - Add full size div for loader.

2. CSS

   - .loader {

     position: fixed;

     z-index: 101;

     width: 100%;

     height: 100%;

     background: linear-gradient(127deg, #a759d1 0%, #8261ee 91%);

     transition: background 350ms ease-in-out;

     }

3. JS

   - Use animate function for loader.
   - When window is loaded, loader call animate function.
   - Keyframes: from opacity: 1 to opacity: 0
   - Option: duration: 1000, easing: 'ease-out'

4. 4/11 github commit

   [https://github.com/wijihye/Web-Designs/commit/07fc257b765f9e2f3532fc410cf35deb59756c50](https://github.com/wijihye/Web-Designs/commit/07fc257b765f9e2f3532fc410cf35deb59756c50)
