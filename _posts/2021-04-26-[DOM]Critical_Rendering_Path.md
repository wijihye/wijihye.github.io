---
layout: post
title: '[DOM] Critical Rendering Path'
tags: [study, dom, document_object_model, rendering_path]
---

#### [DOM] Critical Rendering Path

Date: 2021-04-26

![critical_rendering_path](https://user-images.githubusercontent.com/58647487/116125826-ee9c6e80-a700-11eb-949a-8e0a698c6907.jpg)

---

### Summary

- HTML이 브라우저에서 해석되어 사용자에게 보여지는 과정은 크게 <span style="color:salmon">Construction</span>과 <span style="color:salmon">Operation</span>으로 나눌 수 있다.
  - <span style="color:salmon">Construction:</span> DOM -> CSSOM -> Render Tree
  - <span style="color:salmon">Operation:</span> layout -> paint -> composition
- Operation의 layout과정은 앞의 Render Tree(computed css rules를 가지고 있음.)를 참고해 개략적이고 전체적인 layout을 구성한다. <span style="color:#5733FF;">정확히 어디에 얼마만큼 크게</span> 구성되는지를 결정함.
- Operation의 paint과정은 웹페이지에서 애니메이션이 발생했을 때 layout을 다 그리는 비효율적인 일을 최대한 피하기 위해 <span style="color:#5733FF;">각 요소들을 layer로 분리하여 만듦.</span> => 변경 된 부분에 해당 layer만 다시 그려주면 됨!
- Operation의 composition과정은 앞의 paint과정에서 만들어진 layer들을 z-index에 맞게 쌓아준다. (z-index가 높을수록 나중에 쌓음; 위로 감)
