---
layout: post
title: '[memo] How to write a clean code.'
tags: [study, memo, clean_code, dry, kiss, yagni]
---

### [memo] 깔끔하고 깨끗한 코드 작성하기 방법 -3가지

### DRY (Don't Repeat Yourself)

![DRY](https://user-images.githubusercontent.com/58647487/116848937-ab725c00-ac28-11eb-8819-c3191c2ffc31.jpg)

- 단순히 반복되는 코드만을 피하는 것이 아니고 넓은 의미의 지식, 비즈니스 로직등의 반복 또한 피한다.
- 상황에 따라 각기 다른 에러를 출력하는 if문이 여러 개 있는 것은 괜찮은데, 이유는 **출력**한다는 자체를 반복하고 있기는 하지만 처리하는 로직이 서로 다르기 때문이다.

---

### KISS (Keep  It Simple, Stupid)

![KISS](https://user-images.githubusercontent.com/58647487/116848936-aad9c580-ac28-11eb-92e1-ec230dde12f5.jpg)

- 함수가 늘어나거나 소스가 길어지는 것을 두려워하지 말고  

  <span style="color:yellowgreen; font-weight:800">누구나 한 번에 이해 가능하도록</span>  

  <span style="color:yellowgreen; font-weight:800">한 가지의 기능만을 담당하도록</span>  

  구현할 것.

---

### YAGNI (You Ain't Gonna Need It)

![YAGNI](https://user-images.githubusercontent.com/58647487/116848941-aca38900-ac28-11eb-9d35-964a4fc4460f.jpg)

- 지금 현재 사용하는, 사용할 기능에 초점을 두고 코드를 작성한다.

- 너무 미래지향적이거나 사용하지 않는 기능을 굳이 작성할 필요는 없음!  

  `*사용하지 않는 코드가 생긴다면 주석처리보다는 지워주자!*`