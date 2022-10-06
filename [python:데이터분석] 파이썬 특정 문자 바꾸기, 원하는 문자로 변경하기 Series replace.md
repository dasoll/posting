<!-- [python/데이터분석] 파이썬 특정 문자 바꾸기, 원하는 문자로 변경하기 Series replace  -->

## replace

Series 객체에서 특정 문자를 다른 문자로 바꾸고 싶다면 replace 함수를 이용하면 됩니다.  

<br>

예를 들어, 6,000 이라는 데이터를 콤마(,)를 제거하고 숫자형으로 바꿔야할 경우가 있을 것입니다.

<br>

<div>

~~~python
import pandas as pd

tmp = pd.Series(['5,000', '1,000'])
tmp = tmp.str.replace(',', '')

print(tmp)
~~~
---

</div>

<br>

문자를 일괄 변경할 때 유용한 함수입니다.  
엑셀에서 전체 찾아바꾸기를 하는 것과 동일한 역할을 합니다.

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

마지막에 천단위를 replace를 통해 콤마를 없애고 숫자형으로 변경하였습니다.