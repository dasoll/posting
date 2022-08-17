<!-- [python/크롤링] KB 월간 통계 엑셀 파일 받기 by selenium (1)  -->

## KB 월간 통계 엑셀 파일
KB 부동산 사이트에서 제공하는 월간 통계 엑셀 파일이 있습니다.  
우리나라 부동산 자료 대부분의 원소스라고 볼 수 있고 많은 강의에서도 사용합니다.  
매주, 매달 나오는 데이터를 자동으로 업데이트 하기 위한 첫 걸음으로 엑셀 파일을 받아보겠습니다.  

## selenium으로 KB 월간 통계 사이트 접속
저번 시간에 배운대로 KB 월간 통계를 받을 수 있는 페이지를 실행시켜 보겠습니다.  

---
~~~python
url = "https://kbland.kr/webview.html#/main/statistics?blank=true"
browser = webdriver.Chrome('./chromedriver')
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