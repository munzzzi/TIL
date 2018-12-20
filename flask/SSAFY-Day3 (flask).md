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



```python
from flask import Flask, render_template
app = Flask(__name__)
import random

@app.route("/")
def hello():
    return '''<h1>오잉<h/1>'''
    
    
@app.route("/html_tag")
def html_tag():
    return '''
    <h1>첫번째<h/1>
    <h2>두번째<h/2>
    '''
    
    
@app.route("/html_file")    
def html_file():
    return render_template("html_file.html")
    
@app.route("/welcome/<string:name>")
def welcome(name):
    return render_template("welcome.html",people=name)
    
@app.route("/cube/<int:num>")
def cube(num): 
    return render_template("cube.html",number=num)
    
    
@app.route('/lunch')
def lunch():
    menu=["삼겹살","샤브샤브","치킨","국밥"]
    pick = random.choice(menu)
    return render_template("lunch.html",pick=pick)
    
    
@app.route('/lotto')
def lotto():
    numbers= range(1,46)
    pick=random.sample(numbers,6)
    sort_pick = sorted(pick)
    return render_template("lotto.html", sort_pick=sort_pick )
    
@app.route('/naver')
def naver():
    return render_template("naver.html")
    
    
    
@app.route('/google')
def google():
    return render_template("google.html") 
    
    
@app.route('/wiki')
def wiki():
    return render_template("wiki.html")
    
@app.route('/youtube')
def youtube():
    return render_template("youtube.html")
```





#### github에 올리기

- github에 올리지 말아야할 문서는 .gitignore에 파일명 쓰기
- github 오른쪽위 +누르고 new repository
- repository 만들고 c9으로가기
- git commit -m "~"  > push하기전 주소 넣기 >git push -n..
-   