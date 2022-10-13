<!-- [python/데이터분석] 파이썬 pandas 문자형만, 숫자형만 선택하기 select_dtypes -->

## 문자형, 숫자형 나눠서 전처리

데이터 분석을 진행할 때, Category(범주형)와 Numerical(수치형) 데이터를 구분하여 처리하는 것이 중요합니다. 

<br>

특히 범주형 데이터는 dummy 변수로 변형하거나 Embedding(임베딩)으로 벡터화를 해주어야 모델 학습이 가능합니다.

<br>

왜냐하면 컴퓨터는 숫자만 읽을 수 있기 때문입니다.

## select_dtypes

이처럼 범주형과 수치형을 따로 처리하기 위해서 type별로 데이터를 선택할 수 있는 방법입니다.

<br>

수치형일 경우 float 혹은 int로 입력합니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15], 'F' : ['가','나','다']}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy.select_dtypes('int'))
~~~
---

</div>

<br>
 
범주형일 경우 object로 입력합니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15], 'F' : ['가','나','다']}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy.select_dtypes('object'))
~~~
---

</div>

<br>