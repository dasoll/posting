<!-- [python/크롤링] 네이버 부동산 아파트 매물 크롤링 by requests -->

## 매물 크롤링

저번 포스팅에서는 아파트 정보를 확인해보았습니다.  
(참고 : [[python/크롤링] 네이버 부동산 아파트 정보 크롤링 by requests](https://ssorr.tistory.com/17))  

<br>

이번엔 아파트별 어떤 매물이 있는지 확인해보겠습니다.  

## 매물 API 확인하기

네이버 부동산 아파트 정보 포스팅에서와 같은 요령으로 API를 확인합니다.  
화면에서 단지정보를 누르면 나오는 request가 주르륵 나옵니다.  
그 중에서 ***숫자?realEstateType***로 시작하는 request를 선택합니다.  

<!-- gif -->

preview를 보면 매물 정보가 들어가 있는 것을 확인할 수 있습니다.

## 아파트 정보 응용하기

저번 포스팅에서 아파트 정보 크롤링 결과 중에 markerId도 있었습니다.  
위에서 말한 ***숫자?realEstateType***에서 숫자에 markerId를 넣으면 그 아파트의 매물이 나옵니다.  

<br>

이것을 응용하여 여러개의 아파트의 모든 매물을 한번에 크롤링 해보겠습니다.  

## 코드 작성

~~~python
import requests
import pandas as pd

# 아파트 정보 API
url = 'https://new.land.naver.com/api/complexes/single-markers/2.0?zoom=16&priceType=RETAIL&markerId&markerType&selectedComplexNo&selectedComplexBuildingNo&fakeComplexMarker&realEstateType=APT%3AABYG&tradeType=&tag=%3A%3A%3A%3A%3A%3A%3A%3A&rentPriceMin=0&rentPriceMax=900000000&priceMin=0&priceMax=900000000&areaMin=0&areaMax=900000000&oldBuildYears&recentlyBuildYears&minHouseHoldCount&maxHouseHoldCount&showArticle=false&sameAddressGroup=true&minMaintenanceCost&maxMaintenanceCost&directions=&leftLon=127.22368324725714&rightLon=127.23878978650774&topLat=37.39487323583748&bottomLat=37.37235418956169'

r = requests.get(url)

# 개발자도구에서 request 정보도 입력해주어야 한다. 안그러면 로봇으로 인식해서 에러 발생한다.
r = requests.get(url, headers={
    "Accept-Encoding": "gzip, deflate, br",
    "Host": "new.land.naver.com",
    "Sec-Fetch-Dest": "empty",
    "Sec-Fetch-Mode": "cors",
    "Sec-Fetch-Site": "same-origin",
    "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36"
})

data = r.json()

df_list = []

for apt in data:
    markerId = apt['markerId']

    # 매물 정보 API
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

    df_list.append(df_article)

pd.concat(df_list).to_csv('./tmp.csv', encoding='euc-kr')
~~~
---

pandas를 활용하여 DataFrame을 처리하고 csv로 만드는 과정은 다른 포스팅에서 다루도록 하겠습니다.  

## 크롤링의 기본

결국 크롤링의 기본은 ***API***를 확인하고 ***json 결과를 처리***해주는 것입니다.  
API가 없다면 html 페이지를 beautifulSoup으로 분석할 수도 있습니다.  
그리고 json 처리할 때 DataFrame을 이용하면 더욱 용이합니다.

<br>

기본을 알면 응용이 가능해지니 꾸준히 배워가시기 바랍니다. 화이팅!