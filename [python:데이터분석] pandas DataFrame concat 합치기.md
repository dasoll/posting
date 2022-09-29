<!-- [python/데이터분석] pandas DataFrame concat 합치기 -->

## DataFrame 합치기

데이터분석 도중 DataFrame 여러개를 하나로 합치고 싶을 때가 있습니다.  

<br>

예를 들어, 네이버 부동산 매물 크롤링에서 여러 아파트의 매물들이 나오면 어떻게 해야할까요?  
여러개를 따로따로 저장하고 싶지 않다면 하나의 DataFrame으로 만들어야할 것입니다.  
(참고 : [[python/크롤링] 네이버 부동산 아파트 매물 크롤링 by requests](https://ssorr.tistory.com/18))  

## concat

DataFrame 여러개를 합치고 싶을 때 concat을 사용합니다.  
DataFrame을 수평으로 붙일 수도 있고 수직으로 붙일 수도 있습니다.  

<br>

~~~python
import pandas as pd

tmp_list1 = [[1,2,3,4,5], [6,7,8,9,10]]

tmp_df1 = pd.DataFrame(tmp_list1)

tmp_list2 = [[5,4,3,2,1], [10,9,8,7,6]]

tmp_df2 = pd.DataFrame(tmp_list2)

pd.concat([tmp_df1, tmp_df2])
~~~
---

기본적으로 DataFramee들을 수평으로 붙여줍니다.  

<br>

주의해야할 점은 넣고 싶은 DataFrame들을 list로 만들어서 파라미터로 넣어야 된다는 점입니다.  
콤마로만 연결하면 에러가 발생하니 주의해주세요!

## axis

axis를 1로 바꾸게 되면 수평으로 붙일 수 있습니다.  

<br>

~~~python
pd.concat([tmp_df1, tmp_df2], axis=1)
~~~
---

## 예제 코드

df_list를 만들고 for문을 돌면서 list에 DataFrame을 하나씩 넣습니다.  
for문이 종료되고 concat하면 쉽게 DataFrame을 합쳐줄 수 있습니다.  
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