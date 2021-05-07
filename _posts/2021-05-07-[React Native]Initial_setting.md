---
layout: post
title: '[React Native] 초기 환경설정'
tags: [study, react_native]
---

#### [React Native] 초기 환경설정하기

Date: May 07, 2021

### React Native

- Cross Platform (IOS, Android 모두 개발 가능)
- JS로 동작
- JS, TS 지원

---

### 갑자기 RN?

이번에 thisis RN 팀에서 스터디원을 모집하길래 나도 슬쩍 신청함 ㅋㅋㅋㅋ 스터디듣는사람중에 내가 젤 최고령자임 ..

근데 대충 보니까 어떻게 돌아가는지 알 것 같음 신기하네 .. CSS랑 JS를 조금이라도 할 줄 알기 때문인가?

---

### Github Repo

만들긴 했지만 아직 비공개라 나중에 다시 수정하겠음.

---

### 환경설정하기

진짜 너무너무 힘들었다 이렇게까지 힘들일이야..? 컴퓨터에 깔려있는게 많으니 자기끼리 충돌한 듯.. ㅠㅠㅠ

- 윈도우면

  https://firework-ham.tistory.com/103 ← 참고 (그냥 npm부터 시키는대로 다 해놓자)

  환경변수 설정할 때 시스템 변수 설정하면 됨.

  윈도우에서는 안드로이드밖에 시뮬 안됨 ㅠ

- 안드로이드 스튜디오에서

  - 안드로이드 스튜디오 => SDK Manager

  - 위의 SDK Location 보고 환경변수 설정하면 됨.

    ANDROID_HOME : SDK Location 그대로 작성

    Path의 맨 뒤에 추가할 것 : SDK Location\platform-tools

  - SDK Platforms

    => 알맞는 안드로이드 버전 설치. (나는 10.0 (Q) 설치함)

    => 오른쪽 아래 Show Package Details 클릭

    ✅Intel x86 Atom_64 System Image

    ✅Google APIs Intel x86 Atom System Image

    ✅Google APIs Intel x86 Atom_64 System Image

    ✅Google Play Intel x86 Atom System Image

  - SDK Tools

    ✅Android SDK Build-Tools 31-rc3

    ✅Android SDK Command-line Tools (latest)

    ✅Android Emulator

    ✅Android SDK Platform-Tools

    ✅Google Play Licensing Library

    ✅Intel x86 Emulator Accelerator

  - OK 후 모두 install 하기

- 순서

  1. 원하는 폴더에 cmd로 들어가기 (git bash 상관 X)
  2. react-native init [프로젝트 이름] 해서 프로젝트 생성하기
  3. 프로젝트 폴더로 cd이용해서 들어가기
  4. npm install (node이용위한 기본 세팅)
  5. react-native run-android → 해당 프로젝트 실행하기
  6. 환경변수 및 안드로이드 스튜디오 등이 제대로 설치되었다면 바로 에뮬이 켜진다.

---

### 느낌 및 각오

이왕 시작한거 실무투입 가능할 정도로 해보자. React도 공부해야하고 TS도 공부할거고 다 하면서 공부한 것만이라도 잘할 수 있도록 하는거다!! 목표는 TS로 RN, React.js 다 만들어서 JS, TS, React, React Native, CSS, HTML 다 할 수 있는 사람 되기!

공부한 것들은 아이패드로 손수 필기 할 것이고, 필기한 내용을 캡쳐해서 여기도 올릴거임. 난 손으로 필기해야 되는 스타일이야 아무래도ㅋㅋㅋ
