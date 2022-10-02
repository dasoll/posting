<!-- [python/크롤링/selenium] FRED 경제 데이터 원소스 excel(csv) 가져오기 with 미국채금리 -->

## FRED란?

미국의 세인트루이스 연방준비은행(FED)에서 제공하는 경제 통계 사이트입니다.  
미국의 각종 경제 데이터를 확인할 수 있으며 우리나라에서도 많이 활용하고 있습니다.  

<br>

[FRED 구경하기](https://fred.stlouisfed.org/)

## FRED에서 제공하는 CSV 파일

FRED에서는 각종 경제 통계 데이터의 원소스를 CSV, EXCEL 파일 등으로 제공합니다.  
이것을 다운 받아 분석에 사용할 수 있고 시각화에도 사용할 수 있습니다.  

<br>

참고 : [미국채 장단기 금리차 동향 (2022.09.29)](https://blog.naver.com/eyuki2/222887770506)

## selenium

selenium은 크롬을 이용해 사이트의 각종 요소들을 다룰 수 있는 python library 입니다.  
이것을 활용하여 자동으로 FRED의 데이터를 다운로드 받아 보겠습니다.  

<br>

<div>

~~~python
from selenium import webdriver
from selenium.webdriver.common.by import By
import time
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import shutil
import os

url = "https://fred.stlouisfed.org/series/DGS10"
browser = webdriver.Chrome(
    '/Users/dasolseo/Documents/GitHub/study/크롤링/chromedriver')
browser.get(url)

wait = WebDriverWait(browser, 10)

wait.until(EC.element_to_be_clickable((By.CLASS_NAME, 'graph-footer')))

element = wait.until(EC.element_to_be_clickable((By.ID, 'zoom-all')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-button')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-data-csv')))
element.click()
~~~
---

</div>

<br>

expected_conditions 객체를 이용해 요소가 로딩될 때까지 기다리고 요소를 클릭합니다.  
참고 : [Selenium - 페이지 로딩이 완료될 때까지 기다리기 (python)](https://codechacha.com/ko/selenium-explicit-implicit-wait/)  

<br>

첫번째 graph_footer는 화면이 로딩되고 날짜가 다시 리셋되어서 화면이 전체 로딩되는 것을 기다리기 위해 넣었습니다.  

<br>

zoom-all은 Max 버튼을 눌러 기간을 전체 기간으로 바꿔 줍니다.  

<br>

download_button을 누르고 download-data-csv을 누르면 csv 파일이 받아집니다.  

<br>

각각의 요소의 ID, Class, tag 등을 확인하는 방법은 아래의 글을 참고 부탁드립니다.  
참고 : [[python/크롤링] KB 주간 통계 엑셀 파일 받기 by selenium](https://ssorr.tistory.com/10?category=1028600)

## 전체 예제

10년물 국채금리 뿐만 아니라 2년물, 3개월물까지 받는 전체 코드도 공유드립니다.  

<br>

<div>

~~~python
from selenium import webdriver
from selenium.webdriver.common.by import By
import time
from selenium.webdriver.support.ui import WebDriverWait
from selenium.webdriver.support import expected_conditions as EC
import shutil
import os

url = "https://fred.stlouisfed.org/series/DGS10"
browser = webdriver.Chrome(
    '/Users/dasolseo/Documents/GitHub/study/크롤링/chromedriver')
browser.get(url)

wait = WebDriverWait(browser, 10)

wait.until(EC.element_to_be_clickable((By.CLASS_NAME, 'graph-footer')))

element = wait.until(EC.element_to_be_clickable((By.ID, 'zoom-all')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-button')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-data-csv')))
element.click()

# 2년물 미국채
browser.get('https://fred.stlouisfed.org/series/DGS2')

wait = WebDriverWait(browser, 10)

wait.until(EC.element_to_be_clickable((By.CLASS_NAME, 'graph-footer')))

element = wait.until(EC.element_to_be_clickable((By.ID, 'zoom-all')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-button')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-data-csv')))
element.click()

# 3개월물 미국채
browser.get('https://fred.stlouisfed.org/series/DGS3MO')

wait = WebDriverWait(browser, 10)

wait.until(EC.element_to_be_clickable((By.CLASS_NAME, 'graph-footer')))

element = wait.until(EC.element_to_be_clickable((By.ID, 'zoom-all')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-button')))
element.click()

element = wait.until(EC.element_to_be_clickable((By.ID, 'download-data-csv')))
element.click()

time.sleep(5)

shutil.move(os.path.join('/Users/dasolseo/Downloads', 'DGS10.csv'), os.path.join('/Users/dasolseo/Documents/GitHub/study/economics/bond/data', 'DGS10.csv'))
shutil.move(os.path.join('/Users/dasolseo/Downloads', 'DGS2.csv'), os.path.join('/Users/dasolseo/Documents/GitHub/study/economics/bond/data', 'DGS2.csv'))
shutil.move(os.path.join('/Users/dasolseo/Downloads', 'DGS3MO.csv'), os.path.join('/Users/dasolseo/Documents/GitHub/study/economics/bond/data', 'DGS3MO.csv'))

while(True):
    pass
~~~
---

</div>

<br>