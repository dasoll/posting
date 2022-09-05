<!-- [python/크롤링] KB 주간 통계 엑셀 파일 받기 by selenium -->

## 월간 통계 엑셀 받기
이전 글에서 KB 월간 통계 받는 법에 대해서 살펴보았습니다.  
(<https://ssorr.tistory.com/8>)  
이번엔 다른 탭에 있는 주간 통계를 받아보겠습니다.

## 탭 class 확인하기
이전 글과 동일하게 크롬의 개발자 도구를 이용하여 주간 통계 탭의 ***class***를 확인합니다.  
![sample](https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20KB%20%EC%A3%BC%EA%B0%84%20%ED%86%B5%EA%B3%84%20%EC%97%91%EC%85%80%20%ED%8C%8C%EC%9D%BC%20%EB%B0%9B%EA%B8%B0%20by%20selenium.png?raw=true)

## 탭 이동하기
확인한 class명으로 탭 element를 찾아서 click 합니다.  

---
~~~python
from selenium import webdriver
from selenium.webdriver.common.by import By

url = "https://kbland.kr/webview.html#/main/statistics?blank=true"
browser = webdriver.Chrome('/Users/OOOOO/Documents/GitHub/study/크롤링/chromedriver')
browser.get(url)

element = browser.find_element(By.CLASS_NAME, 'nav-link')
element.click()
~~~
---

## 다운로드 버튼 클릭하기
월간 통계와 마찬가지로 다운로드 element를 click 합니다.

---
~~~python
element = browser.find_element(By.CLASS_NAME, 'btn-download')
element.click()
~~~
---

## 월간, 주간 이어서 다운받기
---
~~~python
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

url = "https://kbland.kr/webview.html#/main/statistics?blank=true"
browser = webdriver.Chrome('/Users/OOOOO/Documents/GitHub/study/크롤링/chromedriver')
browser.get(url)

element = browser.find_element(By.CLASS_NAME, 'btn-download')
element.click()

element = browser.find_element(By.CLASS_NAME, 'nav-link')
element.click()
time.sleep(3)

element = browser.find_element(By.CLASS_NAME, 'btn-download')
element.click()

while(True):
    pass
~~~
---
추가적으로 중간에 sleep으로 잠깐 대기를 넣어주었습니다.  
탭이 다 열리기 전에 다운로드 버튼을 찾으면 에러가 발생하기 때문입니다.  