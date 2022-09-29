<!-- [python/크롤링] os.path splitext 파일명 확장자 분리 -->

## 파일명 구조

우리가 사용하는 파일은 보통 파일 이름과 확장자로 구성되어 있습니다.  
확장자는 파일이 어떤 형식으로 이루어져있는지 알려줍니다.  
응용프로그램(Application)에서 파일을 읽을 때도 확장자를 확인하고 파일을 읽습니다.  

## 파일명 확장자 나누기

이전 포스팅에서 언급했던 xlsx와 xls를 구분하고 싶다면 어떻게 해야할까요?  
확장자를 분리해내고 if문을 통해 확인하면 될 것입니다.  

## splittext

확장자를 분리하기 위해 os.path의 splitext 함수를 활용합니다.  
splitext는 split extension을 줄인 것입니다.  

<br>

<div>

~~~python
import os

os.path.splitext('test.xlsx')
# ('test', '.xlsx')
~~~
---

</div>

<br>

위와 같이 파일명과 확장자를 분리해줍니다.  

## 예제

~~~python
import os
import numpy as np

extensions = []

for dirpath, dirname, filenames in os.walk(path):
    for file in filenames:
        name, extension = os.path.splitext(file)
        extensions.append(extension)

print(np.unique(extensions))
~~~
---

폴더 하위항목들 중에 어떤 확장자가 있는지 찾는 코드입니다.  
확장자를 list에 append(저장)하고 unique 함수를 통해 중복을 제거합니다.  

## 원하는 파일만 옮겨 담기

다음 포스팅에선 원하는 파일만 골라서 다른 폴더에 옮기는 작업을 해보겠습니다.