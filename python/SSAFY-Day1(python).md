# SSAFY-Day1

### 파이썬 코드

#### 안녕

```python
greeting="bong ju!!"

print(greeting)
print(greeting)
print(greeting)
print(greeting)
print(greeting)
```

#### 저녁메뉴

```python
import random
menu=["삼겹살","샤브샤브","치킨","국밥"]
pick = random.choice(menu)
#랜덤으로 뽑을때
print(pick)
```

#### 저녁메뉴번호

```python
import random

# 1. menu 리스트를 만들어주세요.
menu = ['영암매력한우수완점','신전떡볶이 광주수완점','양동통닭','광주식당','회마켓','원조나주곰탕50년']
print(menu[1]) 
#메뉴중 1번에 있는것을 출력
choice = random.choice(menu)
print(choice)

phonebook = {'영암매력한우수완점':'062-383-8118',
            '신전떡볶이 광주수완점':'062-956-2334',
             '양동통닭':'062-471-9277',
             '광주식당':'062-962-8284 ',
             '회마켓':'062-952-2026',
             '원조나주곰탕50년':'062-951-3255'
            }

print(phonebook[choice])
```

#### 광주먼지

```python
import requests
from bs4 import BeautifulSoup
url = 'http://openapi.airkorea.or.kr/openapi/services/rest/ArpltnInforInqireSvc/getCtprvnRltmMesureDnsty?serviceKey=' + key + '&numOfRows=10&pageSize=10&pageNo=1&startPage=1&sidoName=%EA%B4%91%EC%A3%BC&ver=1.3'
request = requests.get(url).text
soup = BeautifulSoup(request,'xml')
dong = soup('item')[7]
location = dong.stationName.text
time = dong.dataTime.text
dust = int(dong.pm10Value.text)
#오선동에서의 미세먼지 농도값을 가져옴

print("{0} 기준 {1}의 미세먼지 농도는 {2}입니다.".format(time,location,dust))
if dust>150:
  print("매우나쁨")
#파이썬은 양옆에 부등호를 쓸수있다.  
elif 80 < dust <=150:
  print("나쁨")
elif 30< dust <=80:
  print("보통")
else:
  print("좋음")


```

#### 로또

```python
import random
#numbers에1부터45넣기
numbers= range(1,46)
a=random.sample(numbers,6)
#오름차순정렬 a.sort()
#내림차순정령 a.sort(reverse=True)
a.sort(reverse=True)
print(a)

```

#### 코스피

```python
import requests
from bs4 import BeautifulSoup

url = "https://finance.naver.com/sise/"
#네이버증권에서 가져옴
r = requests.get(url).text
soup = BeautifulSoup(r,'html.parser')
select = soup.select_one("#KOSPI_now")

print(select.text)

```

