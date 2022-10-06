<!-- [python/데이터분석] 파이썬 특정 문자로 문자열 나누기 (문자 나누기/split)  -->

## split

파이썬에서 문자열을 기준으로 나누려면 split 함수를 사용하면 된다.  
파라미터는 나눌 기준 문자를 지정해주면 된다.  
기본값은 띄어쓰기 입니다.  

<br>

<div>

~~~python
print('1억 6,000'.split())

print('1억 6,000'.split('억 '))
~~~
---

</div>

<br>

1억 6,000을 계산할 수 있도록 16000으로 만들기 위해서는 억단위와 천단위를 구분해야 합니다.  
이런 경우에 split을 이용할 수 있습니다.  

## pandas Series split

Series 객체에서 일괄적으로 split을 적용할 수도 있습니다.

<br>

<div>

~~~python
import pandas as pd

tmp = pd.Series(['1억 2,000', '7억 6,000', '3억 8,000'])

print(tmp.str.split('억 '))

print(tmp.str.split('억 ', expand=True))
~~~
---

</div>

<br>

Series 객체에서 str.split 함수를 사용하면 모든 값에 동일하게 적용할 수 있습니다.  
마찬가지로 나눌 기준 문자를 지정해주면 됩니다.  

<br>

문자열만 있을 때와 다른 점은 expand 파라미터가 있습니다.  
이것은 나눈 후 각각의 컬럼으로 나눌지 여부를 결정합니다.  
위의 결과 값을 보시면 바로 이해가 될 것입니다.  


참고 : <https://pandas.pydata.org/docs/reference/api/pandas.Series.str.html>  

## 예제

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

expand를 이용해 억단위와 천단위를 구분했습니다.  
그리고 각각의 컬럼을 숫자로 바꾼 뒤 다시 더하면 숫자형 가격을 구할 수 있습니다.  