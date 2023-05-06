# naver KOSPI 지수 가져오기
<img width="900" alt="Screenshot 2023-05-06 at 5 45 10 PM" src="https://user-images.githubusercontent.com/83897840/236613672-053cdb81-7b1a-439a-b78a-a65c022997f2.png">
#### 다음과 같이 두 가지 방법으로 해당 지수 가져오겠습니다 -->
<img width="700" alt="Screenshot 2023-05-06 at 5 45 50 PM" src="https://user-images.githubusercontent.com/83897840/236613716-b6f84de3-9bce-47d7-a2c5-dd4e985c6daf.png">

##### 1. span 클래스의 num 이름을 가지는 객체를 가져오는 방법:
```` python
import urllib.request
from bs4 import BeautifulSoup

#네이버 금융 국내증시 메인 사이트 주소
url = "https://finance.naver.com/sise/"

#웹사이트 정보 요청
page = urllib.request.urlopen(url)

# 해당 페이지는 cp949 방식의 인코딩 사용, 다른 웹사이트에서는 보통 'utf8'사용
html = page.read().decode('cp949')

# html.parser 로 html 형식 태그에서 데이터 추출 준비
soup = BeautifulSoup(html, 'html.parser') 

soup.select('span.num')
````
output:
````
[<span class="num _au_real_list">@code@</span>,
 <span class="num num2" id="KOSPI_now">2,500.94</span>,
 <span class="num" id="KOSDAQ_now">845.06</span>,
 <span class="num num2" id="KPI200_now">326.17</span>]
 ````
 ```` python
 soup.select('span.num')[1]
 float(soup.select('span.num')[1].string.replace(',', ''))
  ````
  output:
````
<span class="num num2" id="KOSPI_now">2,500.94</span>
2500.94
````

##### 2. KOSPI.now라는 id의 값을 가져오는 방법:
```` python  

soup.find(id = 'KOSPI_now')

# KOSPI_now 라는 id를 기준으로 크롤링 진행
# id를 기준으로 데이터를 가져올 때는 find 메소드를 사용
 
````
output:
````
<span class="num num2" id="KOSPI_now">2,500.94</span>
````
```` python  

float(soup.find(id = 'KOSPI_now').string.replace(',', ''))
 
````
output:
````
2500.94
````





