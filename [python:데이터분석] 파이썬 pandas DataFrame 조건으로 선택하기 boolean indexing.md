<!-- [python/데이터분석] 파이썬 pandas DataFrame 조건으로 선택하기 boolean indexing -->

## boolean indexing (불리안 인덱싱, 조건으로 선택)

boolean type의 배열(Series, ndarray, list 등)을 통해서 DataFrame의 행을 선택할 수 있습니다.

<br>

이러한 데이터를 선택 방식을 boolean indexing이라고 부릅니다.

<br>

## 특정 조건 데이터만 뽑기

아래의 데이터에서 10 이상의 데이터만 뽑아보겠습니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy[df_copy >= 10])
~~~
---

</div>

<br>

***df_copy >= 10*** 조건문을 컬럼 선택하듯이 대괄호 안에 넣습니다.

<br>

해당 위치의 boolean 값이 True 였던 데이터만 보이게 됩니다.

<br>

나머지는 NaN이 됩니다.

## 컬럼 기준으로 특정 조건 데이터 뽑아내기

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy[df_copy['A'] >= 10])
~~~
---

</div>

<br>

조건문만 ***df_copy['A'] >= 10*** 으로 변경했습니다.

<br>

조건문의 결과가 ***False, False, True*** 이므로 3번째 행만 출력되게 됩니다.

## 배열을 변수로 만들어서 가독성 높이기

조건이 다양해질수록 조건문이 길어질 수 있습니다.

<br>

조건문을 변수로 선언해주면 가독성이 높아집니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

boolean_index = df_copy['A'] >= 10
display(df_copy[boolean_index])
~~~
---

</div>

<br>