<!-- [python/크롤링] 피터팬 매물 크롤링 by requests -->
## 크롤링의 필요성
집을 구할 때, 넓은 범위로 알아보고 싶은 경우, 일일히 지도를 옮겨가며 봐야합니다.  
왜냐하면 아래 사진처럼 넓은 범위는 구 단위, 도 단위로 묶여서 나오기 때문입니다.  
<!-- 이미지 -->
결과를 한눈에 파악하기 위해서는 전체 매물을 받아와야할 것이고 결국 크롤링이 필요하게 됩니다!

## API 확인하기
피터팬 사이트에서 화면을 만들 때 API를 이용하여 데이터를 호출합니다.  
이 API를 찾을 수만 있다면 우리가 데이터를 직접 다룰 수 있게 되는 것입니다.  
<br>

크롬에서 F12를 누르고 개발자도구에 들어가서 화면을 살짝 움직이면 여러개의 request가 생기는 것을 확인할 수 있습니다.  
이 중 "***area?zoomLevel...***" request를 클릭합니다.  
그리고 Headers를 누르면 ***Request*** URL이 나오는데 이것이 API 주소입니다.  
<!-- 동영상1 -->

## API 결과 받아보기
~~~python
import requests

url = 'https://api.peterpanz.com/houses/area?zoomLevel=11&center=%7B%22y%22:37.3759959,%22_lat%22:37.3759959,%22x%22:127.2317726,%22_lng%22:127.2317726%7D&dong=&gungu=&filter=latitude:37.1806704~37.570814%7C%7Clongitude:126.9416648~127.5218803%7C%7CcheckDeposit:999~50000000%7C%7CcheckMonth:999~1000000%7C%7CisManagerFee;%5B%22add%22%5D%7C%7CbuildingType;%5B%22%EB%B9%8C%EB%9D%BC/%EC%A3%BC%ED%83%9D%22,%22%EC%95%84%ED%8C%8C%ED%8A%B8%22,%22%EC%98%A4%ED%94%BC%EC%8A%A4%ED%85%94%22%5D%7C%7CcontractType;%5B%22%EC%9B%94%EC%84%B8%22%5D%7C%7CroomType;%5B%22%ED%88%AC%EB%A3%B8%22,%22%EC%93%B0%EB%A6%AC%EB%A3%B8%22%5D%7C%7CroomCount_etc;%5B%221%EC%B8%B5%20~%205%EC%B8%B5%22,%226%EC%B8%B5%20%EC%9D%B4%EC%83%81%22%5D%7C%7CrealSize;%5B%2211%ED%8F%89%20%EC%9D%B4%EC%83%81%22%5D&&pageSize=90&pageIndex=1'

r = requests.get(url)
print(r)
~~~

위의 코드를 작성하고 실행하면 엄청난 길이의 데이터가 확인됩니다.  
여기서 우리는 방 정보를 확인해야하는데 눈으로 확인하기가 어렵습니다.  
그래서 개발자 도구를 한 번 더 활용해서 어디에 방 데이터가 있는지 확인합니다.  

## 방 데이터 찾기
<!-- 동영상2 -->
Preview 탭을 누르면 ***houses > direct > image, noImage***에 방 정보가 있는 것을 확인할 수 있습니다.  
더 자세히 보면 ***houses > peterVerified, recommend, withoutFee***에도 마찬가지로 image, noImage로 방 정보가 있습니다.  
이 과정에서 저도 이름을 보며 있을 것 같은 아이템들을 눌러가며 찾아낸 것입니다.  
(조금의 노가다는 필요합니다...)  

## 방 데이터 결과 확인하기
~~~python
import requests

url = 'https://api.peterpanz.com/houses/area?zoomLevel=11&center=%7B%22y%22:37.3759959,%22_lat%22:37.3759959,%22x%22:127.2317726,%22_lng%22:127.2317726%7D&dong=&gungu=&filter=latitude:37.1806704~37.570814%7C%7Clongitude:126.9416648~127.5218803%7C%7CcheckDeposit:999~50000000%7C%7CcheckMonth:999~1000000%7C%7CisManagerFee;%5B%22add%22%5D%7C%7CbuildingType;%5B%22%EB%B9%8C%EB%9D%BC/%EC%A3%BC%ED%83%9D%22,%22%EC%95%84%ED%8C%8C%ED%8A%B8%22,%22%EC%98%A4%ED%94%BC%EC%8A%A4%ED%85%94%22%5D%7C%7CcontractType;%5B%22%EC%9B%94%EC%84%B8%22%5D%7C%7CroomType;%5B%22%ED%88%AC%EB%A3%B8%22,%22%EC%93%B0%EB%A6%AC%EB%A3%B8%22%5D%7C%7CroomCount_etc;%5B%221%EC%B8%B5%20~%205%EC%B8%B5%22,%226%EC%B8%B5%20%EC%9D%B4%EC%83%81%22%5D%7C%7CrealSize;%5B%2211%ED%8F%89%20%EC%9D%B4%EC%83%81%22%5D&&pageSize=90&pageIndex=1'

r = requests.get(url)
data = r.json()
houses = data['houses']
direct = houses['direct']
direct_image = direct['image']
print(direct_image[0])

# {'hidx': 13331726, 'attribute': {'created_device': 'web', 'naverVerification': True, 'safeDirectTrade': False, 'withoutFee': False, 'withoutFeeDiscount': 0, 'isZero': False, 'recommend': False, 'isFa': None, 'verificationType': 'N', 'isReported': 0, 'isMyReport': 0, 'smartContract': 1, 'userType': 'user', 'status_code': '0103', 'isOwnerConfirm': 0, 'naverUpdatedAt': '2022-08-29 09:40:03', 'peterVerified': False, 'peterVerifiedCheckVacancyDate': '', 'peterOwnerCheckedAt': None}, 'info': {'temp_address': None, 'vaddr': 0, 'subject': '용인 외대 인프라 형성된 신축 쓰리룸 빌라 (풀옵션)', 'room_count': 3, 'bedroom_count': 3, 'thumbnail': 'https://img.peterpanz.com/photo/20220828/13331726/630b193d6ca01_thumb.jpg', 'created_at': '2022-08-28 16:29:01', 'live_start_date': '2022-08-29 00:00:00', 'is_octop': 0, 'is_half_underground': 0, 'is_multilayer': 0, 'supplied_size': 94.43, 'real_size': 51.96}, 'type': {'contract_type': '월세', 'trade_type': 'direct', 'building_form': '빌라', 'building_type': '빌라/주택', 'building_code': '4146125321102540012000001', 'isCafe': False, 'fa3Code': 0}, 'price': {'monthly_fee': 850000, 'deposit': 50000000, 'maintenance_cost': 38000}, 'floor': {'target': 5, 'total': 5, 'floor_type': 1}, 'location': {'coordinate': {'latitude': '37.3340598906396', 'longitude': '127.252819118823'}, 'address': {'sido': '경기도', 'sigungu': '용인시 처인구', 'dong': '모현읍'}}, 'favorite': False, 'recentView': False, 'additional_options': {'is_new_building': 0, 'have_parking_lot': 0, 'is_full_option': 0, 'have_elevator': 0, 'support_loan': 0, 'allow_pet': 0, 'is_main_road': 0}, 'peterFlag': False}
~~~

direct > image의 첫번째 데이터를 확인하면 위와 같습니다.  

## 최종 크롤링 예제
~~~python
import requests
from datetime import datetime

def run_peterpan():
    now = datetime.now()
    now_date = now.strftime('%Y-%m-%d %H:%M:%S')
    print(f'기준일 : {now_date}')
    print(f'\n################ 피터팬 ################\n')

    url = 'https://api.peterpanz.com/houses/area?zoomLevel=11&center=%7B%22y%22:37.3759959,%22_lat%22:37.3759959,%22x%22:127.2317726,%22_lng%22:127.2317726%7D&dong=&gungu=&filter=latitude:37.1806704~37.570814%7C%7Clongitude:126.9416648~127.5218803%7C%7CcheckDeposit:999~50000000%7C%7CcheckMonth:999~1000000%7C%7CisManagerFee;%5B%22add%22%5D%7C%7CbuildingType;%5B%22%EB%B9%8C%EB%9D%BC/%EC%A3%BC%ED%83%9D%22,%22%EC%95%84%ED%8C%8C%ED%8A%B8%22,%22%EC%98%A4%ED%94%BC%EC%8A%A4%ED%85%94%22%5D%7C%7CcontractType;%5B%22%EC%9B%94%EC%84%B8%22%5D%7C%7CroomType;%5B%22%ED%88%AC%EB%A3%B8%22,%22%EC%93%B0%EB%A6%AC%EB%A3%B8%22%5D%7C%7CroomCount_etc;%5B%221%EC%B8%B5%20~%205%EC%B8%B5%22,%226%EC%B8%B5%20%EC%9D%B4%EC%83%81%22%5D%7C%7CrealSize;%5B%2211%ED%8F%89%20%EC%9D%B4%EC%83%81%22%5D&&pageSize=90&pageIndex=1'

    for i in range(1,100):
        tmp_url = url.replace('pageIndex=1', f'pageIndex={i}')

        r = requests.get(tmp_url)

        data = r.json()
        if len(data) == 0:
            break
        houses = data['houses']
        lst_houses = []
        for key in houses.keys():
            lst_houses.append(houses[key])

        for house in lst_houses:
            for key in house.keys():
                rooms = house[key]

                for row in rooms:
                    info = row['info']
                    subject = info['subject']
                    room_count = info['room_count']
                    size = str(round(info['real_size']/3.3)) + '/' + str(round(info['supplied_size']/3.3))

                    types = row['type']
                    contract_type = types['contract_type']
                    building_form = types['building_form']

                    prices = row['price']
                    total_fee = str(round(int(prices['monthly_fee'])/10000) + round(int(prices['maintenance_cost'])/10000))
                    deposit = str(round(int(prices['deposit'])/10000))

                    floors = row['floor']
                    floor = str(floors['target']) + '/' + str(floors['total'])

                    address = row['location']['address']
                    total_address = '{0} {1} {2}'.format(address['sido'], address['sigungu'], address['dong'])

                    id = row['hidx']
                    print(f'{total_address}, {subject}, {room_count}룸, {size}평, {building_form}' + 
                        f', {deposit}/{total_fee}, {floor}층, https://www.peterpanz.com/house/{id}')

run_peterpan()
~~~

houses의 모든 데이터를 for문으로 확인하고 image, noImage도 for문을 돌면서 확인합니다.  
나머지는 필요한 부분을 받아서 print 해주는 코드입니다.  
궁금하신 점 있으면 언제든 댓글 남겨주세요!