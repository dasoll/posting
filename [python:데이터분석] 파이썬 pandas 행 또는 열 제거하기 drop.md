<!-- [python/데이터분석] 파이썬 pandas 행 또는 열 제거하기 drop -->

## 불필요한 행 또는 열 제거하기

데이터프레임에서 행이나 열을 제거할 수 있습니다.

<br>

index나 컬럼을 직접 지정해주면 됩니다.

## 행 제거하기

index를 단독값이나 list 형태로 입력하면 됩니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15], 'F' : ['가','나','다']}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy.drop(1))
display(df_copy.drop([0,1]))
~~~
---

</div>

## 열 제거하기

열을 제거할 때는 axis 파라미터를 지정해줘야 합니다.

<br>

drop 함수의 기본 axis 값은 0이고 열을 제거하기 위해선 1을 입력해야 합니다.  

<br>

axis가 0일 때는 행방향, 1일 때는 열방향이라고 기억하시면 좋습니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15], 'F' : ['가','나','다']}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy.drop('A', axis=1))
display(df_copy.drop(['B','D'], axis=1))
~~~
---

</div>

<br>