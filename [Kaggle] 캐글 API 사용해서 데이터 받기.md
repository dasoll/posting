<!-- [Kaggle] 캐글 API 사용해서 데이터 받기 -->
## Kaggle API란?
Kaggle API란 Kaggle competition에서 사용하는 데이터를 사용자가 직접 저장하는 방식이 아닌 kaggle 라이브러리를 통해 스크립트에서 바로 저장하는 방식입니다.

## 설치 방법
---
~~~python
pip install kaggle
~~~
---
위의 명령어를 통해 kaggle 라이브러리를 설치합니다.

## 에러
---
~~~
OSError: Could not find kaggle.json. Make sure it's located in /Users/dasolseo/.kaggle. Or use the environment method.
~~~
---
처음에 라이브러리만 설치하고 바로 API 호출 커맨드를 입력하면 (Kaggle 페이지에서 복사해서 사용할 수 있음) 위와 같은 에러가 발생할 것입니다.  
위 에러는 kaggle 계정 인증이 되지 않아서 발생하는 에러로 계정 인증을 해야만 사용할 수 있습니다.

## 계정 인증
1. 홈페이지 우측 상단의 프로필 클릭
2. Account 클릭
3. 화면 중단의 ***Create New API Token*** 클릭
4. ***kaggle.json*** 파일을 ***/Users/{유저명}}/.kaggle*** 폴더로 이동

## Data 다운로드
Kaggle Competition의 Data 탭에서 중단의 API copy 버튼을 누르면 아래와 같이 명령어가 복사됩니다.

---
~~~python
!kaggle competitions download -c tabular-playground-series-aug-2022
~~~
---
Jpyter notebook에서 위 명령어를 입력하면 notebook이 있는 디렉토리에 압축된 데이터(.zip 파일)를 받을 수 있습니다.  
보통 notebook이 저장된 상위폴더(input)에 데이터를 저장합니다.

## 예시 코드
---
~~~python
import pandas as pd

train = pd.read_csv('../input/tabular-playground-series-aug-2022/train.csv')
test = pd.read_csv('../input/tabular-playground-series-aug-2022/test.csv')
~~~
---
