---
layout: post
title: '[work] Excel 파일 업로드해서 읽기'
tags: [work, server, database, db]

---

#### Date: June 16, 2021

### HTML

```html
<form enctype="multipart/form-data" action="test.py" method="post">
	<input type="file" class="file" accept=".xlsx" name="File" value="">
	<input type="submit" value="제출">
</form>
```

- form 태그와 input type="file"을 이용함.
- form의 enctype을 꼭 "multipart/form-data"로 지정해 주어야 file이나 img를 서버로 전송할 수 있다.
- input의 accept 속성은 업로드 될 파일의 형식을 결정한다.

### Python

```python
import pandas as pd

form = cgi.FieldStorage()
File = form['File']

if File.filename:
    file_name = os.path.basename(File.filename)
    open('/tmp/'+file_name, 'wb').write(File.file.read())
    # open한 결과를 변수에 담지는 X
    # 파일이 임시 업로드 되었기 때문에 /tmp/ 경로에 쌓인다.
    # open 안의 경로를 열고 안의 내용을 읽어온 내용으로 채운다. (overwrite)
    
    SO_excel = pd.read_excel('/tmp/'+file_name)
    print(SO_excel.to_html(justify='center', index=False)
```

- pandas, xlrd(pandas.read_excel 시 필요) 모듈 별도 설치 필요.
- read_excel에 매우 많은 옵션(속성)이 필요함. 알아보기.
- excel을 읽어오면 dataframe 형식으로 저장함. to_html함수를 이용해 웹에 `<table>` 형식으로 뿌려준다.