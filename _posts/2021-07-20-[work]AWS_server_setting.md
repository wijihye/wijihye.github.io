---
layout: post
title: '[work] AWS 서버 구축 및 도메인 연결'
tags: [work, server, aws]
---

#### Initial Posted Date: July 20, 2021

### AWS 서버 생성 및 도메인 연결

1. AWS를 기업용으로 가입한 후 인스턴스에 용량 500Gib의 인스턴스를 생성한다.
2. Elastic IP를 만들어서 인스턴스에 고정 IP를 할당한다.
3. AWS의 Route53을 이용해 DNS를 변경하고 SSL 인증을 통해 HTTPS를 연결해준다.
   - [참고 1: 도메인 구입, 연결, HTTPS 연결](https://brunch.co.kr/@skykamja24/287)
   - [참고 2: 도메인 설명, 도메인 연결, HTTPS 연결, 이메일 발송 위한 도메인 인증](https://musma.github.io/2019/09/16/what-to-do-after-you-buy-your-new-domain-on-aws.html)

4. 주의
   1. DNS변경 시 NS 주소의 맨 뒷 . 을 포함하여 저장하는 바람에 계속 오류가 떴었다.. 
   2. TTL을 봐야 한다. 최대 48시간까지 걸린다고 한다.

### 서버 구축 (마지막 수정 21-07-20)

1. apache2 설치

   ```
   1. sudo apt-get update
   2. apt-get install apache2
   ```
    -> <strong>21-07-20:</strong> 도메인 설정 후 15시간 정도밖에 지나지 않아서 그런가 SSL(Xshell) 및 SFTP(Filezilla)는 접속이 되고, apache2도 정상적으로 동작하는 것 같은데 막상 홈페이지에서 연결은 안된다 ㅠㅠㅠ
    <br>
    -> <strong>21-07-21:</strong> 도메인 네임서버를 잘못 연결함. 맨 끝의 .까지 같이 등록하니까 안됐던 것. 이후로는 문제없이 잘 됨.
    <br>

2. root 사용자 비밀번호 만들고 기본 설정하기

   ```text
   1. sudo passwd (root) 후 패스워드 입력
   2. sudo vi /etc/ssh/sshd_config
       i 눌러서 편집모드 들어간 후 PermitRootLogin 을 yes로 만들기 → 
       esc눌러 다시 명령모드로 들어가 :wq 입력해 빠져나오기. (:set nu 입력하면 라인 번호 나옴)
   3. sudo mkdir /roor/.ssh
   4. sudo cp /home/[ubuntu or 초기 로그인 이름]/.ssh/authorized_keys /root/.ssh
   5. sudo service sshd restart
   6. 다음부터 root로 login 가능
   ```

   

3. .pem 없이 서버에 접속하기 <span style="color:red;">(최초 접속 시에는 .pem 필요!)</span>

   ```
   1. (유저생성 해도 되고 그냥 root로 해도 됨) 
       1. sudo useradd -s /bin/bash -m -d /home/[UserName] -g root [UserName]
   2. 유저 비밀번호 생성
       1. sudo passwd [UserName]
   3. sudoers 파일에서 권한 변경
       1. sudo chmod u+w /etc/sudoers
   4. sudoers 파일에 유저 추가
       1. sudo vi /etc/sudoers
       2. i
       3. [UserName] All=(All:All)
       4. esc
       5. :wq
   5. PasswordAuthentication 설정 변경
       1. sudo vi /etc/ssh/sshd_config
       2. i
       3. PasswordAuthentication no → yes
       4. esc
       5. :wq
   6. sudo service ssh restart
   ```

4. .py 웹 구동시키기

   ```
   1. a2enmod cgi // cgi 켜기
   2. sudo vi /etc/apache2/sites-enabled/000-default.conf
       로 들어가 i(편집하기)를 이용해 DocumentRoot 밑에 
       
       <Directory /var/www/html>
       AddHandler cgi-script .py
       Options ExecCGI
       </Directory>
       
       직접 치고 esc로 편집을 마친 후 :wq로 저장하고 빠져나오기.
   3. sudo service apache2 restart
   4. python3 -V
   5. sudo apt-get install python3-pip
   6. sudo pip install [모듈 이름]
   7.  파이썬에서 기본 설정 코드들 넣어준 후 파일 권한 설정하고 제대로 나오는지 확인하기
   ```

5. Maria DB 설치하기

   1. cat /etc/issue : Ubuntu 버전 확인하기

   2. [Maria DB - install](https://downloads.mariadb.org/mariadb/repositories/#mirror=rackspace)에 접속 후 알맞은 버전 고르기

   3. 알맞은 버전 고르고 따라하기

   4. 설치 후 root 비밀번호 최초 설정하기

      ```
      - sudo mysql
      - SELECT user,authentication_string,plugin,host FROM mysql.user;
      - SET PASSWORD FOR 'root'@'localhost' = PASSWORD('new_password');
      - FLUSH PRIVILEGES;
      ```

6. 만약 service apache2 restart가 제대로 작동하지 않는다면
    ```
    4번에서 편집기를 이용해 친 내용을 붙여넣기하게 되면 운영체제 간에
    특수문자를 표시하는 방법이 달라서 그럴 수 있으니 붙여넣기 말고 직접
    쳐서 하기. -> 후에 다시 restart 해보고 service apache2 status
    ```