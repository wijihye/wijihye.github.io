---
layout: post
title: '[thisis] 앱에서 기능 끄고 켜기 관리'
tags: [work, thisis]
---

#### thisis - 앱에서 기능 끄고 켜기 관리

Date: Mar 10, 2021

1. 개발한 것
   - DB table에서 select 해 온 정보로 json 출력
   - 정적 페이지
   - DB table
2. 개발 이유
   - thisis 앱에서 각 기능을 간편하게 끄고 켤 수 있게 관리 위해서
3. 설명
   - 오른쪽의 정적 페이지 구현!
   - button은 form으로 감싸서 submit 시에 해당 id를 넘길 수 있도록 함
4. 모습

![on_and_off](https://user-images.githubusercontent.com/58647487/115881681-f4871b00-a486-11eb-8d99-67997806cedd.png)

#### Source

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

cur = db.cursor(pymysql.cursors.DictCursor)
# 전체 on_off 조회
sql_Select_All = f'SELECT * FROM function_on_off'

cur.execute(sql_Select_All)
function_All_Result = cur.fetchall()

#######################################################

print('''
    <!DOCTYPE html>
  <head>
    <meta charset="UTF-8">
    <title>Turn on and off</title>
    <style>
      .on{
      background-color:#98ee99;
      }

      .off{
      background-color:#ff867c;
      }
    </style>
  </head>
  <body>
    <div align = "center">
    <br>
    <h1>기능 끄고 켜기</h1>
    <br>
    <table border = "1">
      <tr>
        <th>id</th>
        <th>function</th>
        <th>on/off</th>
        <th>button</th>
      </tr>
      ''')

for result in function_All_Result:
  if(result['on_off'] == 1):
  status = "ON"
  else:
  status = "OFF"

  print('''
      <tr>
        <td align = "center">'''+str(result['id'])+'''
        <td align = "center">'''+result['function']+'''</td>
        ''')
  if(status == "ON"):
    print('''<td align = "center" class = "on">'''+status+'''</td>''')
  else:
    print('''<td align = "center" class = "off">'''+status+'''</td>''')

  print('''<td align = "center">
              <button onclick = "turnOnandOff(this.form);">전환하기</button>
            </td>
      </tr>
        ''')

print('''
    </table>
  </div>
  </body>
  </html>
    ''')
```

- 기능 끄고 켜는 정적 페이지

![function_on_off](https://user-images.githubusercontent.com/58647487/115881687-f7820b80-a486-11eb-87e3-152f37bd919f.png)

- DB table

![json](https://user-images.githubusercontent.com/58647487/115881686-f650de80-a486-11eb-94ed-7315d63c7dda.png)

- db → json
