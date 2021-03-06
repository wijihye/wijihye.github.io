---
layout: post
title: '[thisis] 기능 켜고 끄기 버튼 세부 구현'
tags: [work, thisis]
---

#### thisis - 기능 켜고 끄기 버튼 세부 구현

Date: Mar 11, 2021

1. 무엇을

   - 전환하기 버튼을 누르면 on/off가 자동으로 바뀌도록

2. 어떻게

   - popup → 관리자 로그인 → 로그인 정보로 해시, 정보확인 →
     - 맞으면: 디비 update → 버튼 페이지 redirect
     - 틀리면: 버튼 페이지 redirect

3. 세부

4. code

##### source1: function_turning_on_and_off.py

![source1](https://user-images.githubusercontent.com/58647487/115884194-9871c600-a489-11eb-8575-0a1ad8b3faa9.png)

```python
# 테이블의 버튼을 form으로 감싸기
print('''<td align = "center">
<form name = "popup_send_id">
<input type = "hidden" name = "rowId" value = '''+str(result['id'])+'''>
<input type = "hidden" name = "rightRoute" value = "yes">
<button onclick = "turnOnandOff(this.form);">전환하기</button>
</form>
</td>
</tr>
''')

# 소스 맨 아래에 script 추가하기
print('''<script>
function turnOnandOff(form){

window.open("popup_function_login.py", "popup_function_login",
"width = 470, height = 180, top = 100, left = 100");

form.target = "popup_function_login";
form.action = "popup_function_login.py";
form.submit();

}

</script>''')
# 추가!
```

- 팝업창 파일 이름: popup_function_login(py)
- 팝업창 target: popup_function_login
- 팝업창 옵션: width, height, top, left ...
- update할 function의 id를 hidden으로 넘기기 위한 form의 target, action을 설정
  ⇒ submit!

##### source2: popup_function_login.py

![source2](https://user-images.githubusercontent.com/58647487/115884202-99a2f300-a489-11eb-9aed-fce5256100a1.png)

```python
#!/usr/bin/python3
# -*- coding: utf-8 -*-
print("Content-type:text/html;charset=utf-8\r\n")

#######################################################

import sys
import codecs
import cgi
import cgitb
import json
import pymysql
sys.path.insert(0,'/var/www/html/thisis_py/db')
from db_proc import db

sys.stdout = codecs.getwriter("utf-8") (sys.stdout.detach())
cgitb.enable()

#######################################################

form = cgi.FieldStorage()
row_Id = form.getvalue('rowId')

####################

print('''<!DOCTYPE html>
<head>
<meta charset="UTF-8">
<title>Check password</title>
</head>
<body>
<div align="center">
<h2>Admin</h2>
<form action = "function_loginCheck.php" method = "post">
<input type="hidden" name="rowId" value='''+row_Id+'''>
<b>ID</b>: <input type="text" name="id"><br>
<b>PW</b>: <input type="password" name="pass"><br><br>
<input type="submit" value="Login">
</form>
</div>
</body>
</html>'''
)
```

- hidden으로 받은 rowId를 또 다른 폼으로 넘기기 위해 hidden으로 또 보냄
- input을 통해 관리자 id, pw를 받아서 function_loginCheck(php)로 넘김

##### source3: function_loginCheck.py

```php
<?php
session_cache_expire(30);
session_start();
include "../../thisis/db/connect.php";

$id = $_POST['id'];
$pass = $_POST['pass'];
$row_Id = $_POST['rowId'];

$sql = "SELECT * FROM Management WHERE id = '".$id."'";
$result = mysqli_query($connect, $sql);
$row = mysqli_fetch_array($result);
$hash = $row['password'];

if(password_verify($pass, $hash)){
$_SESSION['isLogin']=true;
echo '
<!DOCTYPE html>
<head></head>
<body>
<form action="function_update(.py)" method="post" name="form_sending_id">
<input type="hidden" name="rowId" value='.$row_Id.'>
</form>
</body>
<script>
document.form_sending_id.submit();
</script>
</html>
';
}
else{
echo "
<script>
self.close();
alert('아이디 및 비밀번호를 다시 시도하세요');
</script>
";
}
?>
```

- post로 받은 id, pass, rowId를 저장
- Management 테이블에서 id 조회 → 해시처리해서 테이블에 저장된 pw와 form에서 받아온 pw를 password_verify 함수를 통해 비교하여
  - 맞으면 → update위해 id 넘기기
  - 틀리면 → 창 닫고 alert 띄우기

##### source4: function_update.py

```python
#!/usr/bin/python3
# -*- coding: utf-8 -*-
print("Content-type:text/html;charset=utf-8\r\n")

#######################################################

import sys
import codecs
import cgi
import cgitb
import json
import pymysql
sys.path.insert(0,'/var/www/html/thisis_py/db')
from db_proc import db

sys.stdout = codecs.getwriter("utf-8") (sys.stdout.detach())
cgitb.enable()

#######################################################

form = cgi.FieldStorage()
row_Id = form.getvalue('rowId')

###############################

cur = db.cursor(pymysql.cursors.DictCursor)
sql = f'SELECT on_off FROM function_on_off WHERE id = {row_Id}'
cur.execute(sql)

function_On_Off = cur.fetchone()

if(function_On_Off['on_off'] == 1): # on이면
sql = f'UPDATE function_on_off SET on_off = false WHERE id = {row_Id}'
else: # off면
sql = f'UPDATE function_on_off SET on_off = true WHERE id = {row_Id}'

cur.execute(sql)
db.commit()
db.close()

print('''
<script>
alert("변경되었습니다!");
//opener.parent.location="function_turning_on_and_off.py";
window.close();
</script>'''
)
```

- form에서 받아온 id를 통해 해당 열의 on_off를 변경하기
- 변경이 완료되면 alert 띄우고 source1을 새로고침, popup 닫기
