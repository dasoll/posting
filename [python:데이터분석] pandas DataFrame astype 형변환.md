<!-- [python/데이터분석] pandas DataFrame astype 형변환 -->

## type 변환

DataFrame을 생성하면 자체적으로 값들의 type을 지정합니다.  
예를 들어, 1000이 있으면 숫자 1000으로 지정합니다.  

<br>

하지만, DataFrame을 다시 엑셀 파일로 저장하면 숫자 1000은 자동으로 우측 정렬이 됩니다.  
또한 1000.0과 같이 뒤에 소수점이 자동으로 붙습니다.  

<br>

중간 과정에서 계산할 때는 숫자형을 사용해야 합니다.  
하지만, 결과를 저장할 때는 문자형으로 보는 것이 편할 때가 많습니다.  

## DataFrame 형변환 astype

DataFrame에서 astype 함수를 사용하면 한 번에 형변환을 할 수 있습니다.  

<br>

~~~python
import pandas as pd

tmp_list1 = [[1,2,3,4,5], [6,7,8,9,10]]

tmp_df1 = pd.DataFrame(tmp_list1)

tmp_df1.info()

# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 2 entries, 0 to 1
# Data columns (total 5 columns):
#  #   Column  Non-Null Count  Dtype
# ---  ------  --------------  -----
#  0   0       2 non-null      int64
#  1   1       2 non-null      int64
#  2   2       2 non-null      int64
#  3   3       2 non-null      int64
#  4   4       2 non-null      int64
# dtypes: int64(5)
# memory usage: 208.0 bytes
~~~
---

info 메소드를 사용하면 DataFrame의 개략적인 정보를 확인할 수 있습니다.  
int64형의 데이터를 문자형으로 변환해보겠습니다.  

<br>

~~~python
import pandas as pd

tmp_list1 = [[1,2,3,4,5], [6,7,8,9,10]]

tmp_df1 = pd.DataFrame(tmp_list1)

tmp_df1 = tmp_df1.astype('str')

tmp_df1.info()

# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 2 entries, 0 to 1
# Data columns (total 5 columns):
#  #   Column  Non-Null Count  Dtype 
# ---  ------  --------------  ----- 
#  0   0       2 non-null      object
#  1   1       2 non-null      object
#  2   2       2 non-null      object
#  3   3       2 non-null      object
#  4   4       2 non-null      object
# dtypes: object(5)
# memory usage: 208.0+ bytes
~~~
---

object라고 하는 타입이 DataFrame에서는 문자형입니다.

## 사용 예시

크롤링 예제에서 결과물을 문자형으로 출력하기 위해 astype을 사용한 예시입니다.
(참고 : [[python/크롤링] 네이버 부동산 아파트 매물 크롤링 by requests](https://ssorr.tistory.com/18))  

<br>

~~~python
df_list = []

for apt in data:
    markerId = apt['markerId']

    article_url = f'https://new.land.naver.com/api/articles/complex/{markerId}?realEstateType=APT%3AABYG&tradeType=&tag=%3A%3A%3A%3A%3A%3A%3A%3A&rentPriceMin=0&rentPriceMax=900000000&priceMin=0&priceMax=900000000&areaMin=0&areaMax=900000000&oldBuildYears&recentlyBuildYears&minHouseHoldCount&maxHouseHoldCount&showArticle=false&sameAddressGroup=true&minMaintenanceCost&maxMaintenanceCost&priceType=RETAIL&directions=&page=1&complexNo={markerId}&buildingNos=&areaNos=&type=list&order=rank'

    article_r = requests.get(article_url, headers={
        "Accept-Encoding": "gzip, deflate, br",
        "Host": "new.land.naver.com",
        "Referer": "https://new.land.naver.com/complexes",
        "Sec-Fetch-Dest": "empty",
        "Sec-Fetch-Mode": "cors",
        "Sec-Fetch-Site": "same-origin",
        "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36",
        "authorization":"Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IlJFQUxFU1RBVEUiLCJpYXQiOjE2NjE0MzQ2MDksImV4cCI6MTY2MTQ0NTQwOX0.IH0KAkTwLAgX5qgWF1idr52lKBBFBkaTNq1cmXprLdQ"
    })

    tmp = article_r.json()

    df_articleList = pd.DataFrame(tmp['articleList'])

    if len(df_articleList) == 0:
        continue

    df_article = df_articleList[['articleName','realEstateTypeName','tradeTypeName','floorInfo','dealOrWarrantPrc','areaName','area2','buildingName','cpPcArticleUrl']].astype('str')
    # print(df_article['floorInfo'])
    df_list.append(df_article)

pd.concat(df_list)
~~~
---