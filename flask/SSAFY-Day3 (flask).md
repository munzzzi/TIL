# SSAFY-Day3 (flask)

### C9사용하기-웹에서 코딩:https://c9.io (이메일,플라스크)

#### 파이썬3.6.7을 C9에 설치하기

pyenv> github > install > 1>2 bashrc로 변경 >3>4 > 버전확인후($ python -V)> $ pyenv install 3.6.7> $ pyenv global 3.6.7 >  $ pyenv rehash

```python
$ git clone https://github.com/pyenv/pyenv.git ~/.pyenv
$ echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
$ echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
$ echo -e 'if command -v pyenv 1>/dev/null 2>&1; then\n  eval "$(pyenv init -)"\nfi' >> ~/.bashrc
$ exec "$SHELL"
```



#### 이메일 보내기- 

```python
import smtplib
from email.message import EmailMessage

import getpass
password = getpass.getpass('비밀번호머니?')
#비밀번호 안보이게하는 코딩

msg = EmailMessage()
msg['Subject'] = "제목이지롱"
msg['From'] = "fun3440@naver.com"
msg['To'] = "fun3440@gmail.com"
msg.set_content('내용이지롱')

smtp_url = "smtp.naver.com"
smtp_port = 465

s = smtplib.SMTP_SSL(smtp_url, smtp_port)  #보안SSL

s.login('fun3440',password )
s.send_message(msg)
```



#### 파일을 불러와 대량이메일 보내기

```python
import smtplib
import csv
from email.message import EmailMessage

import getpass
password = getpass.getpass('비밀번호머니?')


f = open('pygj.csv','r', encoding='utf-8')
read_csv = csv.reader(f)

smtp_url = "smtp.naver.com"
smtp_port = 465

s = smtplib.SMTP_SSL(smtp_url, smtp_port)  #보안SSL
s.login('fun3440@naver.com',password )

for line in read_csv:
    msg = EmailMessage()
    msg['Subject'] = line[0] + "님에게 보내는 메일입니다."
    msg['From'] = "fun3440@naver.com"
    msg['To'] = line[1]
    msg.set_content('강민지입니다:>' )
    s.send_message(msg)
```





### Flask 사용하기

```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

$ pip install Flask
$ FLASK_APP=hello.py flask run

```



#### github에 올리기

- github에 올리지 말아야할 문서는 .gitignore에 파일명 쓰기
- github 오른쪽위 +누르고 new repository
- repository 만들고 c9으로가기
- git commit -m "~"  > push하기전 주소 넣기 >git push -n..
-   