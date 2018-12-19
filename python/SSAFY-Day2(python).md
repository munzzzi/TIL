# SSAFY-Day2

## Git명령어

- cd 디렉토리이동
- mkdir 디렉토리 생성
- touch 파일생성

```python
#브라우저열기
import webbrowser

q_list = ["bts","아이유","블랙핑크","위너"]

url = "https://www.google.com/search?q="

for q in q_list:

    webbrowser.open(url+q)
    #"https://www.google.com/search?q=bts"
    #"https://www.google.com/search?q=아이유"
    #"https://www.google.com/search?q=브랙핑크"
    #"https://www.google.com/search?q=위너"
```

## web crawling

```python
#실시간 검색어 가져오기
import requests
from bs4 import BeautifulSoup

url = "https://www.daum.net/"
res = requests.get(url).text
#res = requests.get(url)
#res = requests.get(url).text
#res = requests.get(url).status_code

soup = BeautifulSoup(res,'html.parser')
pick = soup.select("#mArticle > div.cmain_tmp > div.section_media > div.hot_issue.issue_mini.hide > div.hotissue_layer > ol > li:nth-of-type(1) > div > div:nth-of-type(1) > span.txt_issue > a")
print(pick)
#.select 문서안에 있는 특정내용을 뽑아줘
#li:nth-of-type(1) li만 두고 삭제하면 1-10위까지 뽑아짐
#print(p.text) 결과중 ><사이에있는 text만 뽑아짐

```

