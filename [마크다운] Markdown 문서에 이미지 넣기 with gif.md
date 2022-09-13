<!-- [마크다운] Markdown 문서에 이미지 넣기 with gif -->
## 마크다운 문서에 이미지 넣기

마크다운에 이미지를 넣는 문법은 간단합니다.  
<br>
~~~
![이미지 제목](이미지 주소)
~~~

## 디렉토리 경로로 이미지 넣기
첫번째로 *.md 문서를 내 PC에서만 사용할 경우의 예시입니다.  
*.md 문서와 같은 디렉토리에 image 폴더를 만들고 폴더 안에 있는 python 로고 이미지를 불러와보겠습니다.  
이 때, 이미지 주소는 그 이미지의 실제 디렉토리 경로가 될 것입니다.

![sample_1](https://github.com/dasoll/posting/blob/main/image/%5B%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4%5D%20Markdown%20%EB%AC%B8%EC%84%9C%EC%97%90%20%EC%9D%B4%EB%AF%B8%EC%A7%80%20%EB%84%A3%EA%B8%B0%20with%20gif_1.png?raw=true)

<br>

~~~python
![image_name](image/python_logo.png)
~~~

<br>

preview에서 이미지가 잘 나오는 것을 확인할 수 있습니다.  

## 웹 마크다운 문서에 이미지 넣기

티스토리와 같은 웹 블로그에서의 마크다운 문서는 어떨까요?  
아무리 디렉토리 경로를 입력해도 이미지가 나오지 않습니다.  
왜냐하면 내 PC의 \*.md 파일이 존재하는게 아니고 ***웹에 문서가 올라간 것***이기 때문이죠.  

<br>

그렇기 때문에 이미지 주소를 디렉토리 경로가 아닌 URL로 입력해야 합니다.  
인터넷은 세계 어디서든 그 주소로 접속할 수 있기 때문입니다!  

## URL 이미지 넣기

~~~python
![image_name](https://github.com/dasoll/posting/blob/main/image/python_logo.png?raw=true)
~~~
<br>

위와 같이 디렉토리 경로만 이미지 주소로 바꿔주면 됩니다.  
저는 주로 github 저장소에 미리 올려둔 이미지 파일을 사용합니다.  
(어디든 인터넷에 올라온 이미지의 주소만 알면 이미지를 넣을 수 있습니다)  

![sample_2](https://github.com/dasoll/posting/blob/main/image/%5B%EB%A7%88%ED%81%AC%EB%8B%A4%EC%9A%B4%5D%20Markdown%20%EB%AC%B8%EC%84%9C%EC%97%90%20%EC%9D%B4%EB%AF%B8%EC%A7%80%20%EB%84%A3%EA%B8%B0%20with%20gif_2.png?raw=true)

## gif 넣기
움짤을 넣을 때도 인터넷에 파일만 올라가 있으면 문제 없습니다.  
문법은 동일하게 사용하고 주소만 gif 이미지 주소를 사용하면 됩니다.  
(동영상 파일을 gif로 변환하는건 다음 포스팅에서 다루겠습니다.)

![펭수](https://t1.daumcdn.net/cfile/tistory/99CC343A5E083F3E23)