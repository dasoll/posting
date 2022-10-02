<!-- [python/크롤링] 네이버 부동산 아파트 호가 최대, 최소 구하기 -->

## 실거래가와 호가

아파트의 실거래가는 실제로 거래된 가격을 이야기 한다.  
실거래가는 호갱노노 같은 사이트에서 보면 보기가 편하다.  
하지만, 거래량이 별로 없는 시기에는 가격이 어떤지 확인하기 애매하다.  

<br>

네이버 부동산의 매물 호가는 시장의 심리를 옅볼 수 있다.  
호가가 매도자, 즉 공급자가 원하는 가격이기 때문이다.  

## 네이버 부동산 아파트 호가 가져오기

아래의 링크를 참조해서 네이버 부동산 아파트 매물 데이터를 가져옵니다.  

<br>

[[python/크롤링] 네이버 부동산 아파트 매물 크롤링 by requests](https://ssorr.tistory.com/18)

## 가격 숫자로 변환하기

받은 데이터의 가격 정보가 0억 0,000 식으로 컴퓨터가 해석할 수 없게 되어있습니다.  
이 데이터를 고쳐서 숫자형 데이터로 만들어주어야 합니다.  

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

## 아파트 평형별 최대, 최소 호가 구하기

매매 데이터만 모아서 84평형의 최대, 최소 호가를 구해보겠습니다.  

<br>

<div>

~~~python
# 매매 데이터만 filter
df = df[df['tradeTypeName'] == '매매']

# 전용 84 평형 데이터만 filter
df_84 = df[(df['area2'] >= 80) & (df['area2'] < 90)]

# 최대, 최소의 index 구해서 filter
df_max = df_84.loc[df_84.groupby('articleName')['dealOrWarrantPrc'].idxmax(), :]
df_min = df_84.loc[df_84.groupby('articleName')['dealOrWarrantPrc'].idxmin(), :]

# 최대 최소 합쳐서 아파트별, 가격별 정렬하기
df_84_minmax = pd.concat([df_max, df_min]).sort_values(by=['articleName', 'dealOrWarrantPrc'], ascending=False)
~~~
---

</div>

<br>

## 결과

최대, 최소가 순서대로 나오고 동일하면 같은 매물이 2번 나오게 됩니다.  

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%B6%80%EB%8F%99%EC%82%B0%20%EC%95%84%ED%8C%8C%ED%8A%B8%20%ED%98%B8%EA%B0%80%20%EC%B5%9C%EB%8C%80,%20%EC%B5%9C%EC%86%8C%20%EA%B5%AC%ED%95%98%EA%B8%B0.png?raw=true' width=600>