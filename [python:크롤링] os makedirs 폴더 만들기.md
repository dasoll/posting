<!-- [python/크롤링] os makedirs 폴더 만들기 -->

## 폴더 만들기

크롤링을 하다보면 결과를 파일로 저장할 때가 생깁니다.  
저장을 하기 위해 폴더를 만들어야 하는데 직접 탐색기에서 만들 수 있습니다.  

<br>

하지만, 자동화를 위해 코드로 작성한다면 더욱 좋겠죠?  

## os makedirs

python에서 기본 제공하는 os 라이브러리를 이용해 폴더를 만들어보겠습니다.  

<br>

<div>
  
~~~python
os.makedirs('./test_folder')

print(os.path.exists('./test_folder'))
~~~
---
  
</div>

<br>

test_folder 라는 폴더를 만들었습니다.  
exists 함수를 통해 잘 만들어졌는지도 확인할 수 있습니다.  

## 이미 존재하는 폴더일 때

<div>
  
~~~python
# ---------------------------------------------------------------------------
# FileExistsError                           Traceback (most recent call last)
# Input In [31], in <cell line: 1>()
# ----> 1 os.makedirs('./test_folder')
#       3 print(os.path.exists('./test_folder'))

# File /opt/anaconda3/envs/py39_64/lib/python3.9/os.py:225, in makedirs(name, mode, exist_ok)
#     223         return
#     224 try:
# --> 225     mkdir(name, mode)
#     226 except OSError:
#     227     # Cannot rely on checking for EEXIST, since the operating system
#     228     # could give priority to other errors like EACCES or EROFS
#     229     if not exist_ok or not path.isdir(name):

# FileExistsError: [Errno 17] File exists: './test_folder'
~~~
---
  
</div>

<br>

위의 코드를 한 번 더 실행시키면 위와 같은 에러가 발생합니다.  
이미 폴더가 존재하기 때문입니다.  

## 중복 제외하고 폴더 만들기

이미 존재하는 폴더를 제외하고 만들기 위해서 새로운 함수가 필요합니다.  
이 함수는 직접 만들어주겠습니다.  

<br>

<div>
  
~~~python
def createDirectory(directory):
    if not os.path.exists(directory):
        os.makedirs(directory)
~~~
---
  
</div>

<br>

이처럼 exists 함수를 활용해 존재하지 않는 폴더만 만들 수 있습니다.