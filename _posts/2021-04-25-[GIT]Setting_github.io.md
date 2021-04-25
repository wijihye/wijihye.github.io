---
layout: post
title: '[GIT] 깃허브 블로그 설정하고 여러 환경설정 하기'
date: 2021-04-25
tags: [study, git]
---

#### [GIT] github.io 생성 및 테마 설정하기 & github.io를 로컬에서 고쳐보기

Date: 2021-04-25

1. **github블로그를 사용하게 된 계기**

- 이론이나 간단한 실습한 것도 잔디를 심고 싶었다. (노션 외에도)

2. **github 블로그 테마 선택하기**

   - 댓글 등의 거창한 기능은 필요 없고, 내가 공부한 것을 하루하루 기록할 수 있는 정도면 되기 때문에 간단한 테마를 고르고자 함.
   - 직전에 선택한 테마는 코드블럭의 색이 예쁘지 않아서 Repository를 만들었다가 삭제하는 바람에 며칠치 commit 이력이 날아가 버렸다 ㅜㅜ
   - 현재 선택한 것이 [Biu-Jekyll-Theme](https://github.com/RedL0tus/Biu-Jekyll-Theme.git)
     - 간단하면서도 년도별 구분이 되어 있음.

3. **활용 계획**

   1. 일단 이 테마 자체는 글이 많아진다고 페이지를 나누어주는 것이 아닌 것 같다.
   2. About 탭에서 했던 프로젝트 및 공부 내용을 검색할 수 있는 태그를 설명해 놓고, 깃 주소가 있으면 표시하는 식으로 요약을 할 예정.
   3. 그러니까 Home에서 글을 찾는 것이 아니고 About, Search 등의 tab으로 글을 다시 보는 식임.
   4. markdown 문법은 많이 공부하긴 했는데 일단 모르는거는 구글링으로 해결하면서 써보려고 함.

4. **로컬에서 글 고치고 블로그 미리보기**

   1. Ruby(32bit) + Devkit 설치

      - 두개 다 설치해야한다.. 루비만 설치하는 블로그 글 따라했다가 거의 5시간 날려먹음 ㅠㅠ

   2. MSYS2 설치하기 (1, 2, 3 모두 엔터하면 된다. Devkit과 함께 설치했다면 설치를 성공적으로 할 수 있음.)

   3. cmd에서 ruby, gem 설치되었는지 확인하기

      `ruby --version`

      `gem --version`

   4. cmd에서 jekyll 및 bundler 설치하기

      `gem install jekyll bundler`

   5. 블로그 세팅 파일 있는 곳으로 이동하기 -> cd 이용

   6. 해당 폴더에서 cmd나 powershell 실행하기

      `bundle exec jekyll serve`

   7. 완성! 주소창에 http://localhost:4000 이용하면 볼 수 있음.

   8. 참고 사이트

      - [jekyll](https://jekyllrb-ko.github.io/docs/installation/windows/) (jekyll 공식 블로그)

5. **여담**

   1. 사실 테마를 3개나 바꿨다..
   2. Ruby 및 Jekyll, HTML Django 템플릿 언어 `/{/% /%/}`가 익숙하지 않았고, Markdown도 처음 접해본 터라 오류가 매우 많이 났다 ... 오랜만에 설치과정에서 살짝 화남ㅋㅋㅋㅋㅋㅋ 깃헙 블로그를 사용해보려면 확실히 코딩 경험이 있는 사람이 해야 인내심 있게 할 수 있을듯..
   3. VSCode Live Server처럼 변경 사항이 실시간으로 보여지도록 하는 것도 있는데, 일단은 그건 나중에 해보도록 하자.
      - [참고 블로그 글](<https://ryureka.github.io/blog/GitHub-%EB%B8%94%EB%A1%9C%EA%B7%B8-%EB%A7%8C%EB%93%A4%EA%B8%B0(3)-%EB%A1%9C%EC%BB%AC-%EC%BB%B4%ED%93%A8%ED%84%B0%EC%97%90%EC%84%9C-%ED%8C%8C%EC%9D%BC-%EB%B3%80%EA%B2%BD%EC%82%AC%ED%95%AD-%EC%A6%89%EC%8B%9C-%EC%A0%81%EC%9A%A9%ED%95%98%EA%B8%B0/#1-node-%EC%84%A4%EC%B9%98-%ED%9B%84-gulp-%EC%84%A4%EC%B9%98>)
   4. markdown은 Typora 에디터를 사용해서 만들기로 함. VScode 대로 했더니 이상하게 되더라 ㅠㅠ
   5. vscode에서는 git commit 및 push 하면 되고, cmd에서 서버 열고 설치 및 업데이트 진행하도록 결정.
