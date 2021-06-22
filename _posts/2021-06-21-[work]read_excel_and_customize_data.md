---
layout: post
title: '[work] Excel에서 필요한 정보만 parse 해 정렬하기'
tags: [work, server, database, db]

---

#### Date: June 21, 2021

### Excel에서 필요한 정보만 parse 하기 - pandas.read_excel 함수의 속성 이용

```python
import pandas as pd

form = cgi.FieldStorage()
File = form['File']

file_path = '/~/~/'
file_name = os.path.basename(File.filename)

excel = pd.read_excel(file_path+file_name, [options])
```

- options
  1. sheet_name=[원하는 Sheet 이름]: 특정 Sheet만 가져올 수 있음. list로 여러 개 가져오기 가능.
  2. usecols=[list]: parse 할 column 명들만 list로 만들어 parse함. (index도 가능)
  3. keep_default_na=[boolean]: False이면 NaN을 ''(emty string)으로 변환함.
  4. header=[int]: 해당 행 위치를 조정해 해당 행의 data를 column title로 지정함. 해당 행 위의 data는 제외.
  5. index_col=[int]: 해당 열 위치를 조정해 해당 열의 data를 row title로 지정함. NoNe이면 title X

---

### 데이터 정렬하기 - NaN 있는 행 삭제 / 열 이름 변경 / 열 순서 변경

1. NaN 있는 행 삭제

   - pandas의 dropna()를 이용한다.

   - 그냥 excel 변수(dataframe)에 dropna는 적용이 안돼서 ''(empty string)을 모두 NaN으로 바꾸고 난 후 dropna()를 실행했다.

     ```python
     import numpy as np
     import pandas as pd
     
     excel = excel.replace('', np.nan).dropna()
     ```

2. 열 이름 변경

   - pandas의 rename() 이용.

   - rename할 column을 dict 형식으로 저장한 후 parameter로 넘겨준다.

     ```python
     change_name_of_header = {'Memo':'Item', 'Other 1':'Pieces'}
     
     excel.rename(columns=change_name_of_header, inplace=True)
     ```

   - 모든 열을 다 dict로 하지 않아도 됨. 바꿀 것만 하면 된다. (key: 원래 열이름, value: 바꿀 열이름)

3. 열 순서 변경

   - 순서가 바뀐 열이름들을 list로 저장하고 이를 그대로 덮어씌운다.

   - ```python
     complete_header = ['Line', 'Item', 'Pieces']
     
     excel = excel[complete_header]
     ```

