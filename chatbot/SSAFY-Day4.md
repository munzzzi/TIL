# SSAFY-Day4

### flask_upgade

```
$ FLASK_APP=app.py flask run --host=$IP --port=$PORT        
```

```python
#이번주 로또와 생성된 로또 비교

from flask import Flask,render_template
import random
import requests
import json
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"
    
@app.route('/lotto')
def lotto():
    url = "https://www.dhlottery.co.kr/common.do?method=getLottoNumber&drwNo=837"
    res = requests.get(url).text
    lotto_dict = json.loads(res)
    print(lotto_dict["drwNoDate"])
    week_num = []
    week_format_num = []
    drwtNo = ["drwtNo1","drwtNo2","drwtNo3","drwtNo4","drwtNo5","drwtNo6"]
    for num in drwtNo:
        number = lotto_dict[num]
        week_num.append(number)
        print(week_num)
    lotto_bonus=lotto_dict["bnusNo"]    
    
    
    for i in range(1,7):
        num = lotto_dict["drwtNo{}".format(i)]
        week_format_num.append(num)
    
    #pick= 우리가 생성한번호
    #week_num = 이번주 당첨번호
    
    
    # num1 = lotto_dict["drwtNo1"]
    # num2 = lotto_dict["drwtNo2"]
    # num3 = lotto_dict["drwtNo3"]
    # num4 = lotto_dict["drwtNo4"]
    # num5 = lotto_dict["drwtNo5"]
    # num6 = lotto_dict["drwtNo6"]
    # print(lotto_dict["drwtNo1"])
    # print(lotto_dict["drwtNo2"])
    # print(lotto_dict["drwtNo3"])
    # print(lotto_dict["drwtNo4"])
    # print(lotto_dict["drwtNo5"])
    # print(lotto_dict["drwtNo6"])
    #print(type(res))
    #print(type(json.loads(res)))
    
    num_list=range(1,46)
    pick = random.sample(num_list,6)
    pick =  [2,25,28,33,31,30,9]
    
    cnt=0
    for n in pick:
        if n in week_num:
            cnt=cnt+1
            print(cnt)
            
    if cnt==6:
        rank=1
    elif cnt==5:
         if lotto_bonus in pick:
            rank=2
         else:
            rank=3
    elif cnt==4:
        rank=4
    elif cnt==3:
        rank=5
    else:
        rank="꼴"
        
    print(rank)
    
   return render_template("lotto.html",lotto=pick, week_num=week_num,week_format_num=week_format_num,cnt=cnt, rank=rank  )    
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>여긴 로또 검증페이지에요~</h1>
    <h4>생성된 번호: {{lotto}}</h4>
    <h3>{{week_num}}</h3>
    <h3>{{cnt}}개 맞았어요~</h3>
    <h4>{{rank}}등!!</h4>
</body>
</html>
```

