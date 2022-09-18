<!-- [python/크롤링] 네이버 부동산 아파트 정보 크롤링 by requests -->

## 네이버 부동산 크롤링

부동산 공부를 하다보면 가장 많이 확인하는 사이트 중 하나가 네이버 부동산입니다.  
호갱노노나 아실은 실거래가 정보가 있지만, 네이버 부동산엔 매물 호가를 확인할 수 있습니다.  

<br>

실제 임장을 떠나기 전에 온라인 임장을 위한 필수 사이트!  
네이버 부동산에서 아파트 정보를 긁어와보겠습니다.

## 네이버 부동산 API 확인하기

크롤링을 위해 네이버 부동산의 API를 먼저 확인해야 합니다.  
다방 크롤링과 마찬가지로 구글 크롬의 개발자 도구를 사용합니다.  
(참고 : [[python/크롤링] 다방 월세 크롤링 by requests](https://ssorr.tistory.com/11))  

<br>

네이버 부동산에서 개발자 도구의 ***Network***를 누르고 지도를 살짝 움직이면 request 결과가 생성 됩니다.  
***2.0?cortarNo***로 시작되는 것을 클릭하고 ***preview***를 확인하면 아파트 정보가 확인됩니다.  

<br>

Headers 탭을 보면 Request URL이 나오는데 이것이 API 주소입니다.  
URL을 브라우저에서 접속하면 json 형태로 결과가 나오는 것을 확인할 수 있습니다.  

<br>

<img src='https://github.com/dasoll/posting/blob/main/gif/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%B6%80%EB%8F%99%EC%82%B0%20%EC%95%84%ED%8C%8C%ED%8A%B8%20%EC%A0%95%EB%B3%B4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20requests_5.gif?raw=true' width="800">

<br>


## API 호출과 에러

~~~python
import requests

url = 'https://new.land.naver.com/api/complexes/single-markers/2.0?cortarNo=1165010600&zoom=17&priceType=RETAIL&markerId&markerType&selectedComplexNo&selectedComplexBuildingNo&fakeComplexMarker&realEstateType=APT%3AJGC%3AABYG&tradeType=&tag=%3A%3A%3A%3A%3A%3A%3A%3A&rentPriceMin=0&rentPriceMax=900000000&priceMin=0&priceMax=900000000&areaMin=0&areaMax=900000000&oldBuildYears&recentlyBuildYears&minHouseHoldCount&maxHouseHoldCount&showArticle=false&sameAddressGroup=false&minMaintenanceCost&maxMaintenanceCost&directions=&leftLon=127.0048357&rightLon=127.0228602&topLat=37.5168882&bottomLat=37.5113566'

r = requests.get(url)
print(r.json())
~~~
---

다방 크롤링을 참고하여 코드를 작성하고 실행시키면 에러가 발생합니다.  

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%B6%80%EB%8F%99%EC%82%B0%20%EC%95%84%ED%8C%8C%ED%8A%B8%20%EC%A0%95%EB%B3%B4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20requests_1.png?raw=true' width="400">

<br>

이유를 확인하기 위해 결과를 text로 출력했습니다.  
내용을 보면 bot으로 감지되어 막힌 것을 확인할 수 있습니다.  

<br>

~~~python
import requests

url = 'https://new.land.naver.com/api/complexes/single-markers/2.0?cortarNo=1165010600&zoom=17&priceType=RETAIL&markerId&markerType&selectedComplexNo&selectedComplexBuildingNo&fakeComplexMarker&realEstateType=APT%3AJGC%3AABYG&tradeType=&tag=%3A%3A%3A%3A%3A%3A%3A%3A&rentPriceMin=0&rentPriceMax=900000000&priceMin=0&priceMax=900000000&areaMin=0&areaMax=900000000&oldBuildYears&recentlyBuildYears&minHouseHoldCount&maxHouseHoldCount&showArticle=false&sameAddressGroup=false&minMaintenanceCost&maxMaintenanceCost&directions=&leftLon=127.0048357&rightLon=127.0228602&topLat=37.5168882&bottomLat=37.5113566'

r = requests.get(url)
print(r.text)
~~~
---

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%B6%80%EB%8F%99%EC%82%B0%20%EC%95%84%ED%8C%8C%ED%8A%B8%20%EC%A0%95%EB%B3%B4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20requests_2.png?raw=true' width="600">

<br>

## Request Headers 함께 전송

bot으로 인식되는 것을 피하기 위해 브라우저로 조회할 때와 동일하게 Request Headers라는 것을 보내야 합니다.  
개발자 도구의 Headers를 내리다보면 확인할 수 있습니다.  

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%B6%80%EB%8F%99%EC%82%B0%20%EC%95%84%ED%8C%8C%ED%8A%B8%20%EC%A0%95%EB%B3%B4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20requests_3.png?raw=true' width="400">

<br>

확인한 내용을 requests의 headers 파라미터에 추가해주면 결과가 나오는 것을 확인할 수 있습니다.  

<br>

~~~python
import requests

url = 'https://new.land.naver.com/api/complexes/single-markers/2.0?cortarNo=1165010600&zoom=17&priceType=RETAIL&markerId&markerType&selectedComplexNo&selectedComplexBuildingNo&fakeComplexMarker&realEstateType=APT%3AJGC%3AABYG&tradeType=&tag=%3A%3A%3A%3A%3A%3A%3A%3A&rentPriceMin=0&rentPriceMax=900000000&priceMin=0&priceMax=900000000&areaMin=0&areaMax=900000000&oldBuildYears&recentlyBuildYears&minHouseHoldCount&maxHouseHoldCount&showArticle=false&sameAddressGroup=false&minMaintenanceCost&maxMaintenanceCost&directions=&leftLon=127.0048357&rightLon=127.0228602&topLat=37.5168882&bottomLat=37.5113566'

r = requests.get(url)

# 개발자도구에서 request 정보도 입력해주어야 한다. 없으면 봇으로 인식해서 에러 발생한다.
r = requests.get(url, headers={
    "Accept-Encoding": "gzip, deflate, br",
    "Host": "new.land.naver.com",
    "Sec-Fetch-Dest": "empty",
    "Sec-Fetch-Mode": "cors",
    "Sec-Fetch-Site": "same-origin",
    "User-Agent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/103.0.0.0 Safari/537.36"
})

data = r.json()
print(data[0])
~~~
---

## 건축연도, 아파트 이름 출력하기

간단하게 건축연도와 아파트 이름을 출력해보겠습니다.  

<br>

~~~python
data = r.json()

df = pd.DataFrame(data)

tmp = df[['completionYearMonth', 'complexName']]

for _, row in tmp.iterrows():
    print(', '.join(row.tolist()))
~~~
---

<br>

<img src='https://github.com/dasoll/posting/blob/main/image/%5Bpython:%ED%81%AC%EB%A1%A4%EB%A7%81%5D%20%EB%84%A4%EC%9D%B4%EB%B2%84%20%EB%B6%80%EB%8F%99%EC%82%B0%20%EC%95%84%ED%8C%8C%ED%8A%B8%20%EC%A0%95%EB%B3%B4%20%ED%81%AC%EB%A1%A4%EB%A7%81%20by%20requests_4.png?raw=true' width="200">

<br>

## 아파트에 대한 자세한 내용은?

다음 포스팅에서 아파트별 매물을 확인하는 방법에 대해 알아보겠습니다.