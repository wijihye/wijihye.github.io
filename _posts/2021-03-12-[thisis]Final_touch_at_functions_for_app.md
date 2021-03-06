---
layout: post
title: '[thisis] 기능 끄고 켜기 마무리'
tags: [work, thisis]
---

#### thisis - 기능 끄고 켜기 마무리

Date: Mar 12, 2021

1.  무엇을

    - 파일이름을 통해 source2, 3, 4에 바로 접근할 경우 source1 (button page)로 redirect 되도록 구현
    - db의 table을 조회해 on_off 정보를 json으로 출력가능하게 함
    - 기존에 id를 hidden으로 넘겨 update를 진행했던 것을 function을 넘겨 update할 수 있도록 함
      - why? 만약 수동으로 열을 삭제 및 추가하면 id 값이 변경되는데 그 id값 보다는 function이름 자체로 넘기는게 나을 듯 싶었다.

2.  어떻게

##### first: 정상적인 루트를 통해 접근할 수 있도록하기

- hidden값으로 첫 페이지부터 끝까지 hidden값으로 rightRoute 변수를 넘겨 주어 끝까지 이 변수가 유지되는지 검사

```python
# add 1
right_Route = form.getvalue('rightRoute')

# add 2
if(function == None or right_Route == None):
print('''
<script>
//location.href = "function_turning_on_and_off.py";
</script>
''')
```

##### second: json출력

```python
#!/usr/bin/python3

# -_- coding: utf-8 -_-

print("Content-type:application/json;charset=utf-8\r\n")

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

sql_Select_All = 'SELECT function, on_off FROM function_on_off'

cur.execute(sql_Select_All)
function_All_Result = cur.fetchall()

#######################################################

for result in function_All_Result:

function_Dict = dict()

function_Keys = [
'home',
'campus_Info',
'my_Info',
'more'
]

function_Values = list()
f_Keys = list()

#홈*-*-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-#

home_Function_Dict = dict()

#디스픽*-*-_-_-_-_-_-_-#

this_Pick_Function_Dict = dict()

#학사일정

this_Pick_Academic_Calendar = result['on_off']
this_Pick_Function_Dict['this_Pick_Academic_Calendar'] = this_Pick_Academic_Calendar

#디스스탑이즈

this_Pick_This_Stop_Is = result['on_off']
this_Pick_Function_Dict['this_Pick_This_Stop_Is'] = this_Pick_This_Stop_Is

#교내식당

this_Pick_Restaurant = result['on_off']
this_Pick_Function_Dict['this_Pick_Restaurant'] = this_Pick_Restaurant

#도서관

this_Pick_Library = result['on_off']
this_Pick_Function_Dict['this_Pick_Library'] = this_Pick_Library

#학교공지*-*-_-_-_-_-_-_-#

school_Notice_Function_Dict = dict()

#학사공지

school_Notice_Academic_Notice = result['on_off']
school_Notice_Function_Dict['school_Notice_Academic_Notice'] = school_Notice_Academic_Notice

#장학공지

school_Notice_Scholarship_Notice = result['on_off']
school_Notice_Function_Dict['school_Notice_Scholarship_Notice'] = school_Notice_Scholarship_Notice

#공지사항

school_Notice_Common_Notice = result['on_off']
school_Notice_Function_Dict['school_Notice_Common_Notice'] = school_Notice_Common_Notice

#즐겨찾기

school_Notice_Book_Mark = result['on_off']
school_Notice_Function_Dict['school_Notice_Book_Mark'] = school_Notice_Book_Mark

#

home_Function_Dict = {
'this_Pick':this_Pick_Function_Dict,
'school_Notice':school_Notice_Function_Dict
}

function_Values.append(home_Function_Dict)

#캠퍼스정보*-*-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-#

campus_Info_Function_Dict = dict()

#가상대학

campus_Info_Online_Class = result['on_off']
campus_Info_Function_Dict['campus_Info_Online_Class'] = campus_Info_Online_Class

#교내지도

campus_Info_Campus_Map = result['on_off']
campus_Info_Function_Dict['campus_Info_Campus_Map'] = campus_Info_Campus_Map

#전화번호

campus_Info_Call_Number = result['on_off']
campus_Info_Function_Dict['campus_Info_Call_Number'] = campus_Info_Call_Number

#동아리

campus_Info_Circle = result['on_off']
campus_Info_Function_Dict['campus_Info_Circle'] = campus_Info_Circle

#이벤트

campus_Info_Event = result['on_off']
campus_Info_Function_Dict['campus_Info_Event'] = campus_Info_Event

#

function_Values.append(campus_Info_Function_Dict)

#마이*-*-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-#

my_Info_Function_Dict = dict()

#학적부

my_Info_Register = result['on_off']
my_Info_Function_Dict['my_Info_Register'] = my_Info_Register

#성적표

my_Info_Grade = result['on_off']
my_Info_Function_Dict['my_Info_Grade'] = my_Info_Grade

#시간표

my_Info_Schedule = result['on_off']
my_Info_Function_Dict['my_Info_Schedule'] = my_Info_Schedule

#장학정보

my_Info_Scholarship = result['on_off']
my_Info_Function_Dict['my_Info_Scholarship'] = my_Info_Scholarship

#위쇼

my_Info_We_Show = result['on_off']
my_Info_Function_Dict['my_Info_We_Show'] = my_Info_We_Show

#외박신청

my_Info_Apply_For_Stay_Out = result['on_off']
my_Info_Function_Dict['my_Info_Apply_For_Stay_Out'] = my_Info_Apply_For_Stay_Out

#

function_Values.append(my_Info_Function_Dict)

#더보기*-*-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-_-#

more_Function_Dict = dict()

#개발자

more_Developer = result['on_off']
more_Function_Dict['more_Developer'] = more_Developer

#

function_Values.append(more_Function_Dict)

######

function_Dict = dict(zip(function_Keys, function_Values))
result = {'function_On_And_Off' : function_Dict}

result_json = json.dumps(result, indent = 4, ensure_ascii = False)
print(result_json)

db.close()
```

#### third: id → function

```python
# 변경
<input type = "hidden" name = "function" value = '''+result['function']+'''>
# or
<input type="hidden" name="function" value='''+function+'''>
```
