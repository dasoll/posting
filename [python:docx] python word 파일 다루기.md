<!-- [python/docx] python word 파일 다루기  -->

## python 크롤링 결과 저장 방법
크롤링한 결과를 저장하는 방법은 여러가지가 있습니다.  
엑셀 파일로 저장할 수도 있고 텍스트 파일로 저장할 수도 있습니다.  
이번 포스팅에서는 편집에 용이한 word 파일로 저장하는 방법에 대해 알아보겠습니다.  

## docx 라이브러리
word 파일로 저장하기 위해서 docx 라이브러리가 필요합니다.  
docx 라이브러리를 이용하여 문서를 만들고 PC에 저장할 수 있습니다.  

## 문서에 결과 추가하기
저번에 포스팅했던 네이버 뉴스 크롤링 예제를 사용하겠습니다.  
제목 결과를 word 파일로 저장해보겠습니다.  
(참고 : [[python/크롤링] 네이버 뉴스 크롤링 by BeautifulSoup4(bs4)](https://ssorr.tistory.com/15))  

~~~python
import bs4
import requests
import os
from docx import Document
from docx.shared import Pt

doc = Document()

#스타일 적용하기
style = doc.styles['Normal']
style.font.size = Pt(13)
font = style.font
font.name = 'Malgun Gothic (본문 한글)'

url = 'https://media.naver.com/press/009/newspaper'

r = requests.get(url)

soup = bs4.BeautifulSoup(r.text, 'lxml')

paragraphs = soup.select(".newspaper_brick_item")

for paragraph in paragraphs:
    page_name = paragraph.select('h3')[0].text # A1면, A2면, ...
    doc.add_paragraph(page_name)
    for title in paragraph.select('strong'):
        doc.add_paragraph('제목 : ' + title.text)
        doc.add_paragraph('')
~~~
---

doc 객체를 만들고 글씨체와 크기를 변경해줍니다.  
글씨 크기는 Pt 객체를 별도로 import 해야 합니다.  

## word 파일로 저장하기
doc 객체에 담긴 결과를 save로 저장하면 끝입니다.  

~~~python
doc.save('./news_title.docx')
~~~
---