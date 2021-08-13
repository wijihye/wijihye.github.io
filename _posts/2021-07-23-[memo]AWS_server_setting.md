---
layout: post
title: '[memo] AWS EC2로 서버 구축하고 도메인 연결 및 HTTPS 연결'
tags: [memo, server, aws]
---

### 요약

- 인스턴스 시작
- Elastic IP 등록 및 연결
- 도메인 연결
- SSL 인증 후 HTTPS 연결하기

---

1. 인스턴스 시작
   1. 인스턴스 시작 누르고 설정 쭉
   2. 보안 그룹에서 인바운드 규칙에 80(HTTP), 22(SSH), 443(HTTPS) 모두 열어준 보안 그룹을 연결해야 함.
   3. 루트 말고 다른 저장공간 추가하면 SSH쉘에서 mount 해 주어야 한다.
2. Elastic IP 등록 및 연결
   1. 탄력적 IP 주소를 할당하고, 해당 IP를 서버(인스턴스)에 연결하여 고정 IP를 생성해 준다.
3. 도메인 연결
   1. Route 53 서비스에 접속하여 도메인 연결

4. SSL 인증 후 HTTPS 연결
   - [참고1 - SSL 인증서 발급 + HTTPS 연결](https://developer111.tistory.com/21?category=926455)
   - [참고2 - SSL 인증서 발급 + HTTPS 연결](https://brunch.co.kr/@skykamja24/287)
   - 참고1을 보고 적용함. 도메인 여러 개에 (domain.com and www.domain.com) 적용하고 싶으면 A 레코드를 각 도메인마다 추가해주자. (로드밸런서 연결)