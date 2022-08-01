## 마크다운의 장점
마크다운의 장점은 \*.md 파일로 글을 편집하고 저장할 수 있다는 장점이 있습니다.
즉, 오프라인에서도 글을 작성하고 로컬에 저장해둔 뒤 필요할 때 업로드할 수 있다는 장점이 있습니다.
블로그 글을 온라인에 올려두면 글이 사라질 가능성이 0.01%라도 있지만 나의 로컬 드라이브에 저장해두면 더욱 안전하게 보관할 수 있습니다.
(비트코인의 콜드체인 렛져와 비슷하다고 보면 될까요?)
<br>
그렇다면 티스토리에서 마크다운을 사용하는 방법에 대해 알아보겠습니다.

## 스킨 편집에서 cdn 링크 연결하기

<br>

블로그 관리 > 꾸미기 > 스킨편집 순으로 화면에 진입합니다.  
화면에서 **html 편집**을 클릭합니다.
<br>

***
```html
<link href="https://cdnjs.cloudflare.com/ajax/libs/github-markdown-css/5.1.0/github-markdown-light.css" rel="stylesheet">
```
***
<br>

위의 태그를 **<head>** ... **</head>** 태그 안에 넣으면 됩니다.  

<br>

## 마크다운 모드로 작성
글 작성할 때, 우측 상단의 모드를 마크다운 모드로 작성합니다.  

<br>

## 본문 작성 후 div 태그 추가하기
글을 다 작성한 후, 모드를 **HTML** 모드로 다시 변경합니다.  
HTML 모드에서 최상단을 markdown-body div 태그로 감싸주면 끝입니다.
<br>
***
```html
<div class="markdown-body">
... 본문 ...
</div>
```
***

<br>

## 참고 URL
깃헙 cdn 주소 : https://cdnjs.com/libraries/github-markdown-css  
민곰 즐거워 블로그 : https://behabit.tistory.com/entry/Markdown-티스토리-마크다운-Github-스타일-적용하기