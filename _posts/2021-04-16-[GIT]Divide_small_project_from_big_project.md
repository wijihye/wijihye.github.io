---
layout: post
title: '[GIT] 큰 프로젝트에서 작은 프로젝트 분리하기'
tags: [study, git]
---

### [git]

Date: Apr 16, 2021

#### 하고자 한 것

큰 프로젝트에서 프로젝트를 커밋 이력들과함께 개별 repo로 분리하기

#### 순서

1. 원래 큰 프로젝트 깃에서 softy pinko 프로젝트를 커밋 이력과 함께 분리하기로 함.

2. 분리하고자 하는 가장 큰 프로젝트의 root로 감.

   cd [root]

3. 서브 프로젝트 분리

   git subtree split -P [디렉토리 혹은 파일 경로, 루트부터 시작해서 감. ex) app1/ 하면 app1 아래에 있는 모든 파일이 분리됨.] -b [분리하는 브랜치 이름(아무거나 해도 상관 X)]

4. 디렉토리 만들고 이동

   mkdir [경로 + 폴더이름] && [경로 + 폴더이름]

5. 깃 초기화

   git init

6. 생성한 브랜치 복사하기

   git pull [생성한 브랜치 이름(위에서 만든 것)]

7. 원격 저장소 연결 후 push

   git remote add origin [새 repo 주소]

   git push -u origin main

8. 큰 프로젝트에서 서브 디렉토리 삭제하기 (삭제 이력 남음)

   git rm -rf [디렉토리]

9. 참고 사이트:

   1. [http://sigpoll.blogspot.com/2013/08/git-subtree.html](http://sigpoll.blogspot.com/2013/08/git-subtree.html)

   2. [https://syki66.github.io/blog/2020/09/12/git-subtree.html](https://syki66.github.io/blog/2020/09/12/git-subtree.html)

   3. [https://stackoverflow.com/questions/359424/detach-move-subdirectory-into-separate-git-repository/17864475#17864475](https://stackoverflow.com/questions/359424/detach-move-subdirectory-into-separate-git-repository/17864475#17864475)

#### git 리드미 작성 (마크다운 사용법)

1. 참고사이트: [https://gist.github.com/ihoneymon/652be052a0727ad59601](https://gist.github.com/ihoneymon/652be052a0727ad59601)

2. 첫 ReadMe는 [softy pinko]의 ReadMe를 작성함.

   [https://github.com/wijihye/softy-pinko](https://github.com/wijihye/softy-pinko)
