<!-- [python/데이터분석] 파이썬 pandas DataFrame loc 함수 -->

## DataFrame 원하는 row, column 선택하기 (데이터프레임 행, 열 선택하기)

데이터 프레임을 조작할 때 원하는 부분만 선택하고 싶을 때가 있을 것입니다.  

<br>

이번엔 데이터 프레임의 특정 부분을 선택하는 방법에 대해서 알아보겠습니다.  

<br>

사실 데이터프레임의 특정 범위 선택이 필요하다 싶으면  

<br>

***loc, iloc*** 방법만 사용해서 데이터프레임의 데이터를 선택합니다.


## 1개 데이터 선택하기

특정 행, 렬을 지정하여 1개만 선택하는 방법입니다.  

<br>

loc를 사용하게 되면 컬럼명과 index명을 명시해줘야 합니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)

display(df)

display(df.loc[0, 'A'])
~~~
---

</div>

<br>

순서는 행, 열 순서로 써줘야 합니다. 

## 범위 지정하여 선택하기 (슬라이싱, slicing)

다음은 콜론을 이용하여 범위를 지정하여 선택하는 방법입니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)

display(df)

display(df.loc[0:1, 'A':'D'])
~~~
---

</div>

<br>

이렇게 범위로 지정하는 것을 슬라이싱이라고 합니다.

<br>

## 전체와 일부 선택하기​

전체 행의 특정 열을 지정하거나 전체 열의 특정 행을 지정할 때는 아래와 같이 전체를 슬라이싱 할 수 있습니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)

display(df)

display(df.loc[:, 'A':'D'])

display(df.loc[0:1, :])
~~~
---

</div>

<br>

## 특정 몇개만 선택하기 (list 활용)

또한 리스트를 이용하여 개별 행과 열을 지정할 수도 있습니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)

display(df)

display(df.loc[[1,2], ['A','D']])
~~~
---

</div>

<br>

## 선택한 데이터 일괄 변경

선택한 범위의 값을 일괄로 변경할 수 있습니다.  

<br>

이렇게 변경하면 원본 데이터프레임이 바로 변하기 때문에 

<br>

원본이 손상되길 원하지 않는다면 copy() 함수를 이용하여 새로운 데이터프레임을 만들고 진행하면 됩니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df)

df_copy.loc[:, 'A':'C'] = 'some_value'

display(df_copy)
~~~
---

</div>

<br>

