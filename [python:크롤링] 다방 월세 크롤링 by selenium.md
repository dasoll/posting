<!-- [python/크롤링] 다방 월세 크롤링 by requests -->

## 다방 크롤링이란?
지도로 보면 지역별 매물을 쉽게 찾아볼 수 있지만 넓은 지역의 원하는 조건의 매물을 찾을 땐 불편함이 있다.  
크롤링을 이용하면 넓은 범위의 매물을 받아와 한눈에 확인할 수 있다.  

## 다방 API 확인하기
다방의 API를 먼저 확인해야 한다.  
KB 시세 다운로드와 마찬가지로 구글 크롬의 개발자 도구를 사용한다.  
(참고 : <https://ssorr.tistory.com/8?category=1028600>)  
<br>
다방 검색 화면에서 개발자 도구의 ***Network***를 누르고 지도를 살짝 움직이면 조회가 된다.  
bbox로 시작되는 것을 클릭하면 Request URL이 나오는데 이것을 주소창에 치면 json 형태로 결과가 나오는 것을 확인할 수 있다.  

## URL 살펴보기
API를 보면 URL 인코딩이 되어있어 알아보기 어렵다.  
이것을 디코딩해서 보면 아래와 같다.  (참고 : <https://ssorr.tistory.com/9>)
~~~ python
https://www.dabangapp.com/api/3/marker/multi-room?api_version=3.0.1&call_type=web&filters={"multi_room_type":[3],"selling_type":[0],"deposit_range":[0,5000],"price_range":[0,999999],"trade_range":[0,999999],"maintenance_cost_range":[0,999999],"room_size":[0,999999],"supply_space_range":[0,999999],"room_floor_multi":[1,2,3,4,5,6,7,-1,0],"division":false,"duplex":false,"room_type":[],"use_approval_date_range":[0,999999],"parking_average_range":[0,999999],"household_num_range":[0,999999],"parking":false,"short_lease":false,"full_option":false,"built_in":false,"elevator":false,"balcony":false,"safety":false,"pano":false,"deal_type":[0,1]}&location=[[126.9719818,37.2200389],[127.5212982,37.5316083]]&version=1&zoom=11
~~~

여기서 조건들과 위도, 경도, zoom을 설정하면 원하는 데이터를 가져올 수 있다.  
팁이 있다면 직접 URL을 수정하는 것도 좋지만 원하는 조건을 다방에서 선택한 다음 조회해서 API를 가져오는 것이 쉽다.

## json 처리하기
***requests***를 통해 주소창에 친 것처럼 주소를 요청하고 결과를 받아와서 처리한다.  
json()을 통해 json으로 변경하고 우리가 원하는 방의 데이터를 얻기 위해 ***rooms***를 불러온다.  
rooms에서 한개씩 데이터를 불러오고 마지막에 print하는 작업을 반복한다.  
마지막 주소는 id를 통해 해당 주소를 호출하면 상세화면이 나오기 때문에 추가했다.  

~~~ python
import requests

url = 'https://www.dabangapp.com/api/3/room/list/multi-room/bbox?api_version=3.0.1&call_type=web&filters=%7B%22multi_room_type%22%3A%5B3%5D%2C%22selling_type%22%3A%5B0%5D%2C%22deposit_range%22%3A%5B0%2C5000%5D%2C%22price_range%22%3A%5B0%2C100%5D%2C%22trade_range%22%3A%5B0%2C999999%5D%2C%22maintenance_cost_range%22%3A%5B0%2C999999%5D%2C%22room_size%22%3A%5B0%2C999999%5D%2C%22supply_space_range%22%3A%5B0%2C999999%5D%2C%22room_floor_multi%22%3A%5B1%2C2%2C3%2C4%2C5%2C6%2C7%2C-1%2C0%5D%2C%22division%22%3Afalse%2C%22duplex%22%3Afalse%2C%22room_type%22%3A%5B%5D%2C%22use_approval_date_range%22%3A%5B0%2C999999%5D%2C%22parking_average_range%22%3A%5B0%2C999999%5D%2C%22household_num_range%22%3A%5B0%2C999999%5D%2C%22parking%22%3Afalse%2C%22short_lease%22%3Afalse%2C%22full_option%22%3Afalse%2C%22built_in%22%3Afalse%2C%22elevator%22%3Afalse%2C%22balcony%22%3Afalse%2C%22safety%22%3Afalse%2C%22pano%22%3Afalse%2C%22deal_type%22%3A%5B0%2C1%5D%7D&location=%5B%5B126.9568756%2C37.2266001%5D%2C%5B127.506192%2C37.5381423%5D%5D&page=1&version=1&zoom=11'
r = requests.get(url)

data = r.json()
rooms = data['rooms']

for row in rooms:
    title = row['title']
    room_type_str = row['room_type_str']
    room_desc = row['room_desc']
    room_desc2 = row['room_desc2']
    price_title = row['price_title']
    selling_type_str = row['selling_type_str']
    is_direct = '직거래' if row['is_direct'] == True else '부동산'
    id = row['id']
    print(f'{title}, {room_type_str}, {room_desc}, ' + 
        f'{price_title}, {selling_type_str}, {is_direct}, https://www.dabangapp.com/room/{id}')
~~~

