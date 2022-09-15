<!-- [python/크롤링] 네이버 뉴스 크롤링 by BeautifulSoup4(bs4)  -->
## 네이버 뉴스 구조와 크롤링 목적

네이버 뉴스의 신문보기를 누르면 기사 제목이 카드 형식으로 연속적으로 나옵니다. 
제목만 보고 사유하는 연습을 하기 위해 제목을 추출하는 크롤링을 만들었습니다. 

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%89%B4%EC%8A%A4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20BeautifulSoup4(bs4)_1.png?raw=true' width="400">

<!-- ![image_1](https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%89%B4%EC%8A%A4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20BeautifulSoup4(bs4)_1.png?raw=true) -->

## BeautifulSoup 이용하여 html 추출
requests와 bs4 라이브러리를 이용하여 html을 추출해보겠습니다.  

~~~python
url = 'https://media.naver.com/press/009/newspaper'

r = requests.get(url)
soup = bs4.BeautifulSoup(r.text, 'lxml')
~~~
---
이렇게 하면 soup 객체에 html 정보가 담기게 됩니다.  

## 페이지 css 분석
분석하고 싶은 곳에서 우클릭 후 검사를 누르면 크롬의 개발자 도구가 실행됩니다.  
그리고 우클릭 했던 지점의 css를 바로 확인할 수 있습니다.  

![gif_2](https://github.com/dasoll/posting/blob/main/gif/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%89%B4%EC%8A%A4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20BeautifulSoup4(bs4)_2.gif?raw=true)


<br>

우선 단락의 class명이 newspaper_brick_item인 것을 기억해둡시다.

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%89%B4%EC%8A%A4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20BeautifulSoup4(bs4)_3.png?raw=true' width="700">

## css selector
bs4의 select 메소드를 이용하여 css 요소를 선택할 수 있습니다.  
(참고 : [BeautifulSoup4 Document](https://www.crummy.com/software/BeautifulSoup/bs4/doc.ko/#:~:text=%EB%82%98%ED%83%80%EB%82%98%EB%8A%94%20%EA%B2%83%EC%9D%B4%20%EB%8B%B9%EC%97%B0%ED%95%98%EB%8B%A4.-,CSS%20%EC%84%A0%ED%83%9D%EC%9E%90,-%C2%B6))  
그 중에서 class명으로 요소를 찾기 위해선 아래와 같은 코드를 사용하면 됩니다.  

~~~python
paragraphs = soup.select(".newspaper_brick_item")
~~~
---
이제 paragraphs에는 A1면, A2면, ... 의 면들이 들어있는 객체가 됩니다.  

## 페이지와 제목 추출하기
마지막으로 paragraphs를 돌며 페이지 이름과 제목을 추출합니다.  

~~~python
for paragraph in paragraphs:
    page_name = paragraph.select('h3')[0].text # A1면, A2면, ...
    print(page_name)
    for title in paragraph.select('strong'):
        print('제목 : ' + title.text)
        print('')
~~~
---
h3 태그에 페이지 이름이 들어가 있고 strong 태그에 제목이 들어가있습니다.  

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%89%B4%EC%8A%A4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20BeautifulSoup4(bs4)_4.png?raw=true' width="400">

## Word 파일로 만들기
다음 포스팅에서 위의 결과를 쉽게 사용할 수 있도록 Word 파일로 만들어 보겠습니다.