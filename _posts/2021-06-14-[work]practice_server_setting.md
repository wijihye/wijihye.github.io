---
layout: post
title: '[work] 서버 세팅 연습하기'
tags: [work, server, database, db]

---

### Date: June 14, 2021

### work info

 미국에 파이프 보온재 만드는 회사 에서 Job Boss라는 생산재고관리 프로그램을 쓰는데 회사랑 너무 안맞아서 간단한 기능만 있어도 되니까 맞춤으로 구현하려고 함.

 먼저 Quick Book 프로그램으로 Sales Order를 Excel로 만들면, 그 파일을 업로드 해 자동으로 읽은 후 Inventory에 몇 개 있는지, 생산되는 데 걸리는 예상시간 등을 자동으로 보여줄 수 있게끔 할 것임. (웹에 띄워서 하기)

사용 언어: Python으로 대부분 구현 예정. 거의 백엔드 쪽 성능 중심임.

### Today's Job

 아직 서버를 자체로 구축할지 클라우드로 구축할지 정해지지 않았지만, 그래도 해야 할 일은 비슷하니까 내가 연습용으로 파놓은 클라우드 서버에 구축연습함.

1. root 계정으로 접속할 수 있도록 권한 설정하기
2. apache 설치: 웹으로 띄우기 위함 + .py 웹 세팅
3. python 모듈들 설치
   1. sudo apt-get install python3-pip
   2. sudo pip install [모듈 이름]
4. maria db 설치

