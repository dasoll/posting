<!-- [python/크롤링] 위도, 경도로 주소 찾기 by geopy -->

## 위도, 경도 주소 찾기가 필요한 경우
이전 포스팅에서 살펴보았던 다방 크롤링에서 주소 데이터가 없었습니다.  
(참고 : <https://ssorr.tistory.com/11>)
API에 위도, 경도만 있고 주소는 굳이 전달하지 않는 것입니다.  
우리는 주소로 보는 것이 편하기 때문에 위도, 경로도 주소 찾기가 필요합니다.  

## geopy
geopy는 python에서 geo 코딩을 도와주는 웹서비스입니다.  
(참고 : <https://geopy.readthedocs.io/en/stable/>)

## 예시
~~~python
from geopy.geocoders import Nominatim

def geocoding_reverse(lat_lng_str): 
    geolocoder = Nominatim(user_agent = 'South Korea', timeout=None)
    address = geolocoder.reverse(lat_lng_str)
    address = address[0].split(', ')
    address.reverse()
    address = ' '.join(address[2:])
    return address

latitude = '37.25198576849052'
longitude = '127.54197915686228'

lat_lon_str = ', '.join([latitude, longitude])

address = geocoding_reverse(lat_lon_str)
print(address)
~~~

Nominatim 객체를 이용해 간단하게 함수로 구현하였습니다.  
미국식이기 때문에 주소가 뒤집어져 있는데 이것을 나누고 순서를 바꾼 뒤 다시 붙여주었습니다. ***(split, reverse, join)***  
라이브러리 특성상 위도와 경도를 콤마(,)로 이어준 것도 특징입니다.




