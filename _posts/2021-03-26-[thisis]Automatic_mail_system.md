---
layout: post
title: '[thisis] 건의사항 및 회의 불참여부 자동 메일보내기'
tags: [work, thisis]
---

#### thisis - 건의사항 및 회의 불참여부 자동 메일보내기

Date: Mar 26, 2021

건의사항을 등록하는 페이지가 있고, 회의 불참 여부를 등록하는 페이지가 있다. 이 각각의 내용을 form으로 전송 후 db에 저장하고, 그 db의 table을 조회하여 웹에 뿌리면 확인이 가능한 형태로 구현이 이미 되어 있었다. 그러나 매번 그 페이지로 접속해야하는 번거로움에 팀장이 나에게 일을 맡겼다.

"자동으로 건의사항/회의불참 여부가 등록되면 동시에 팀 gmail로 알림이 오도록 하자!"

이미 우리 서버가 구축되어 있기 때문에 Postfix를 설치하여 SMTP를 구축해 메일을 보낼 수 있도록 하려고 했다. 그러나 생각보다 복잡했다..

먼저, 우리 도메인을 사용하여 구축된 서버에서 메일을 자체적으로 보내기 위해서는 서버가 인증이 되어야하며 그 인증된 서버를 화이트 도메인에 등록 어쩌고,, SPF record 어쩌고.. 모르겠다..

일단 기능자체의 구현을 위해 서버구축은 잠시 뒤로 밀어두고 python의 smtplib을 이용하여 자동 메일 보내기를 만들었다.

html에서 form으로 무엇이든 전송하면 그 전송 내역을 받아서 일단 저장하고 지금 DSIS의 dsisdevteam@gmail.com계정의 SMTP 서버를 빌려 전송하도록 했다. (그래서 sender: dsisdevteam@gmail.com → receiver: dsisdevteam@gmail.com이기 때문에 '나에게보내기' 처럼 보임 ㅠㅠ)

1. gmail의 IMAP 사용하기 설정
2. 해당 계정의 2단계 인증 + 앱 비밀번호 설정(앱 선택: 메일, 기기 선택: 직접추가하기: dsisteam@dsisdevteam.com)
3. python 소스에서 아래 내용 추가하기

   ```python
   # lib 추가
   import smtplib
   from email.mime.text import MIMEText

   # 메일보내기
   today = datetime.now()
   today = today.strftime('%Y-%m-%d')

   send_Mail = smtplib.SMTP('smtp.gmail.com', 587)
   # 사용할 SMTP(host, port)
   send_Mail.starttls()
   # tls
   send_Mail.login('dsisdevteam@gmail.com', ~~'앱 비밀번호'~~)
   # 메일 서버 로그인

   mail_Contents = MIMEText(f'사유 입력일: {today} 사유:{reason}')
   # 메일내용 적기

   mail_Contents['Subject'] = f'[DSIS] 회의 불참: {name}'
   # 메일제목 설정
   send_Mail.sendmail('dsisdevteam@gmail.com', 'dsisdevteam@gmail.com', mail_Contents.as_string())
   # 보내는사람, 받는사람, 메일객체를 string으로 변환

   send_Mail.quit()
   # 메일 연결 종료
   ```

4. 메일이 정상적으로 보내졌는지 확인

일단 기능은 이런 식으로 구현했으나 우리 도메인을 이용해서 보낼수있도록 서버 구축을 알아봐야겠다.. 너무 어려워 ㅠㅠ

21-03-27까지 알아낸 것 정리

[https://www.notion.so/SMTP-7cf5767360bd4b23908a3a1b78c5430f](https://www.notion.so/SMTP-7cf5767360bd4b23908a3a1b78c5430f)

---

SMTP, POP3, IMAP 등에 대해 공부해보자.. SSL, SASL, TCP계층, Port 번호 등 알아갈게 너무 많군
