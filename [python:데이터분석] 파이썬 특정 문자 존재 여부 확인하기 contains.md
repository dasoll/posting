<!-- [python/데이터분석] 파이썬 특정 문자 존재 여부 확인하기 Series contains  -->

## contains

Series 객체에서 특정 문자가 포함된 데이터만 확인하고 싶다면 contains 함수를 이용하면 됩니다.  

<br>

예를 들어, 1억 6,000 이라는 데이터가 있고 5,000 이라는 데이터가 있다고 가정해봅시다.  
1억 6,000 -> 16000, 5,000 -> 5000 으로 바꾸기 위해서는 억이 들어간 데이터와 억이 없는 데이터가 구분되어야 합니다.  

<br>

<div>

~~~python
import pandas as pd

tmp = pd.Series(['1억 2,000', '7억 6,000', '3억 8,000', '5,000', '1,000'])

print(tmp.str.contains('억'))

boolean_index = tmp.str.contains('억')

print(tmp[boolean_index])
~~~
---

</div>

<br>

contains 함수를 이용하면 True, False의 Boolean index가 반환됩니다.  
Boolean index로 Series를 다시 indexing 하면 우리가 원하는 억 데이터가 나옵니다.  

<br>

Boolean index는 mask, filter 등 다양하게 표현됩니다.  
데이터 분석에서 자주 사용되는 방식이니 익혀두시면 좋습니다.  
기회가 되면 boolean index 관련된 포스팅도 남기도록 하겠습니다.  

## 에제

저번 포스팅에서 다루었던 네이버 부동산 아파트 호가 최대, 최소 구하기 예제입니다.  
참고 : [[python/크롤링] 네이버 부동산 아파트 호가 최대, 최소 구하기](https://ssorr.tistory.com/28)

<br>

<div>

~~~python
import pandas as pd

# 데이터 불러오기
df = pd.read_csv('tmp.csv', encoding='euc-kr', index_col=0).reset_index(drop=True)

# 억을 포함하는 가격 데이터 선정
df_over_billion = df[df['dealOrWarrantPrc'].str.contains('억')]

# 억을 기준으로 문자열을 쪼개고 억은 10000을 곱한다.
billion = df_over_billion['dealOrWarrantPrc'].str.split('억', expand=True)[0].astype('int') * 10000
thousand = df_over_billion['dealOrWarrantPrc'].str.split('억', expand=True)[1]

# 천 단위는 콤마를 포함하고 있기 때문에 제거한다.
thousand = thousand.map(lambda x: '0' if x == '' else x).str.replace(',', '').astype('int')

# 변환한 값을 가격 컬럼에 다시 넣는다.
df['dealOrWarrantPrc'] = billion + thousand
~~~
---

</div>

<br>

억을 포함하는 데이터만 따로 뽑아서 숫자 데이터로 변경하기 위해 contains를 사용했습니다.  
가장 직관적으로 필요한 데이터를 찾을 수 있는 방법 중 하나입니다.