<!-- [python/크롤링] os walk 폴더 탐색하기 -->

## 파일 찾기

예를 들어, xls와 xlsx 파일을 다르게 처리해야 한다면?  
이럴 때, walk 함수를 이용해 폴더의 파일을 탐색하고 이름을 불러올 수 있습니다.  

## os walk

<div>

~~~python
for dir_path, dir_names, file_names in os.walk('탐색할 경로'):
    print(dir_path, dir_names, file_names, '\n')
~~~
---

</div>

<br>

특정 폴더의모든 하위항목을 찾을 수 있습니다.  
for문을 사용하면 경로, 폴더이름, 파일이름 순으로 반환하게 됩니다.  

<br>

경로는 string, 폴더이름과 파일이름은 list 형태로 나옵니다.  

## 모든 파일 확인하기

<div>

~~~python
for dir_path, dir_names, file_names in os.walk('/Users/dasolseo/Documents/GitHub/posting'):
    for file_name in file_names:
        print(file_name)
~~~
---

</div>

<br>

탐색한 파일이름에서 한번 더 for문을 활용하면 모든 file을 찾을 수 있습니다.  

## 확장자 검색하기

처음에 예시로 말했던 확장자 구분을 쉽게하는 방법이 있습니다.  
다음 포스팅에서는 파일명과 확장자를 분리해보겠습니다.

<!-- 다음엔 splittext 쓰고 링크 -->