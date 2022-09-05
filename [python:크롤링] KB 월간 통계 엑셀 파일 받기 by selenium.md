<!-- [python/크롤링] KB 월간 통계 엑셀 파일 받기 by selenium  -->

## KB 월간 통계 엑셀 파일
KB 부동산 사이트에서 제공하는 월간 통계 엑셀 파일이 있습니다.  
우리나라 부동산 자료 대부분의 원소스라고 볼 수 있고 많은 강의에서도 사용합니다.  
매주, 매달 나오는 데이터를 자동으로 업데이트 하기 위한 첫 걸음으로 엑셀 파일을 받아보겠습니다.  

## selenium으로 KB 월간 통계 사이트 접속
저번 시간에 배운대로 KB 월간 통계를 받을 수 있는 페이지를 실행시켜 보겠습니다.  

---
~~~python
url = "https://kbland.kr/webview.html#/main/statistics?blank=true"
browser = webdriver.Chrome('/Users/OOOOO/Documents/GitHub/study/크롤링/chromedriver')
browser.get(url)

while(True):
    pass
~~~
---
코드가 종료되면 chrome 창이 자동으로 종료됩니다.  
따라서, 코드가 종료되지 않도록 while문을 활용해 막아주었습니다.  

## 크롬 개발자 도구
이제 다운로드 버튼을 누르는 작업을 해보겠습니다.  
버튼을 찾기 위해선 크롬의 개발자 도구가 필요합니다.  
크롬을 띄우고 ***F12***를 누르면 아래와 같은 화면이 뜹니다.  
여기서 ***Elements*** Tab에서 버튼을 찾아보겠습니다. 

![sample](https://github.com/dasoll/posting/blob/main/image/KB%20월간%20통계%20엑셀%20파일%20받기%20by%20selenium%20(1).png?raw=true)

## 다운로드 버튼 찾기
Elements 창에서 커서를 움직여보면 왼쪽의 화면에 색이 칠해지는 것을 볼 수 있습니다.  
커서가 올려져있는 코드가 화면에서 어떤 곳을 구현하고 있는지 보여주는 것입니다.  
![sample2](https://github.com/dasoll/posting/blob/main/image/KB%20%EC%9B%94%EA%B0%84%20%ED%86%B5%EA%B3%84%20%EC%97%91%EC%85%80%20%ED%8C%8C%EC%9D%BC%20%EB%B0%9B%EA%B8%B0%20by%20selenium_2.png?raw=true)
우리가 찾고자 하는 다운로드 버튼을 향해서 계속 하위 목록을 펼쳐줍니다.  
계속 찾다보면 우리가 원하는 다운로드 버튼을 찾을 수 있습니다.  
버튼 요소의 이름은 ***btn-download***라는 것을 확인할 수 있습니다.  
![sample3](https://github.com/dasoll/posting/blob/main/image/KB%20%EC%9B%94%EA%B0%84%20%ED%86%B5%EA%B3%84%20%EC%97%91%EC%85%80%20%ED%8C%8C%EC%9D%BC%20%EB%B0%9B%EA%B8%B0%20by%20selenium_3.png?raw=true)

## 다운로드 버튼 클릭
---
~~~python
element = browser.find_element(By.CLASS_NAME, 'btn-download')
element.click()
# time.sleep(10)
~~~
---
find_element 메소드를 이용하여 우리가 찾고자 하는 버튼을 찾습니다.  
마지막으로 click 메소드를 이용하여 클릭하면 다운로드가 시작됩니다.  
다운로드 되는 동안 창이 꺼지면 안되기 때문에 sleep 메소드를 이용하여 10초간 대기합니다.  
우리는 이미 while문을 통해 chrome이 종료되지 않도록 해두었기 때문에 주석처리 해두었습니다.  

## selenium 설치
selenium 설치 및 환경설정은 아래의 글을 참고해주세요!  
<https://ssorr.tistory.com/7>