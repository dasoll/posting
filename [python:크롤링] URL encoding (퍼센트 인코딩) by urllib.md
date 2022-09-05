<!-- [python/크롤링] URL encoding (퍼센트 인코딩) by urllib -->

## URL encoding
***퍼센트(%) 인코딩***이라고도 불리우며 URL의 파라미터에 포함된 문자를 표현할 때 사용하는 인코딩 방법입니다.  
영어, 숫자 등의 몇몇 문자를 제외한 나머지 문자를 1바이트 단위로 묶인 16진수로 인코딩합니다.  
URL은 ASCII 코드값만 사용하기 때문에 파라미터에 한글이 포함될 경우, ASCII 코드만으로 표현을 할 수 없어 인코딩이 필요합니다.  

## 디코딩 방법
일반적으로 우리가 크롤링할 때, 개발자도구에서 찾은 api는 인코딩이 된 상태일 것입니다.  
파라미터를 살펴보기 위해 우선 ***urllib.parse 라이브러리의 unquote*** 메소드를 사용해 디코딩이 필요합니다.

---
~~~python
from urllib import parse

url_decode = parse.unquote("https://api.peterpanz.com/houses/area?zoomLevel=11&center=%7B%22y%22:37.3012038,%22_lat%22:37.3012038,%22x%22:127.2389823,%22_lng%22:127.2389823%7D&dong=&gungu=&filter=latitude:37.1056841~37.4962165%7C%7Clongitude:126.9488746~127.5290901%7C%7CcheckDeposit:999~50000000%7C%7CcheckMonth:999~800000%7C%7CisManagerFee;%5B%22add%22%5D%7C%7CbuildingType;%5B%22%EB%B9%8C%EB%9D%BC/%EC%A3%BC%ED%83%9D%22,%22%EC%95%84%ED%8C%8C%ED%8A%B8%22,%22%EC%98%A4%ED%94%BC%EC%8A%A4%ED%85%94%22%5D%7C%7CcontractType;%5B%22%EC%9B%94%EC%84%B8%22%5D%7C%7CroomType;%5B%22%ED%88%AC%EB%A3%B8%22,%22%EC%93%B0%EB%A6%AC%EB%A3%B8%22%5D%7C%7CroomCount_etc;%5B%221%EC%B8%B5%20~%205%EC%B8%B5%22,%226%EC%B8%B5%20%EC%9D%B4%EC%83%81%22%5D%7C%7CrealSize;%5B%2211%ED%8F%89%20%EC%9D%B4%EC%83%81%22%5D&&pageSize=90&pageIndex=1")
print(url_decode)
# https://api.peterpanz.com/houses/area?zoomLevel=11&center={"y":37.3012038,"_lat":37.3012038,"x":127.2389823,"_lng":127.2389823}&dong=&gungu=&filter=latitude:37.1056841~37.4962165||longitude:126.9488746~127.5290901||checkDeposit:999~50000000||checkMonth:999~800000||isManagerFee;["add"]||buildingType;["빌라/주택","아파트","오피스텔"]||contractType;["월세"]||roomType;["투룸","쓰리룸"]||roomCount_etc;["1층 ~ 5층","6층 이상"]||realSize;["11평 이상"]&&pageSize=90&pageIndex=1
~~~
---
피터팬의 방구하기에서 찾은 API 예시입니다.  
디코딩을 하면 한글로된 파라미터를 찾을 수 있고 원하는대로 수정도 가능합니다.  

## 인코딩 방법
파라미터를 수정했다면 다시 인코딩을 통해 호출 가능한 URL을 만들어야 합니다.  
parse 라이브러리의 urlparse를 통해 url을 파싱하고 그 중 query, 즉 파라미터 부분만 다시 인코딩 해줍니다.  
이후, 앞의 주소는 그대로 복원한 뒤 최종 결과를 만들어냅니다.  

---
~~~python
url = parse.urlparse(url_decode)
query = parse.parse_qs(url.query)
result = parse.urlencode(query, doseq=True)

print(query)
print(f'{url.scheme}://{url.netloc}/{url.path}?{result}')
# https://api.peterpanz.com//houses/area?zoomLevel=11&center=%7B%22y%22%3A37.3012038%2C%22_lat%22%3A37.3012038%2C%22x%22%3A127.2389823%2C%22_lng%22%3A127.2389823%7D&filter=latitude%3A37.1056841~37.4962165%7C%7Clongitude%3A126.9488746~127.5290901%7C%7CcheckDeposit%3A999~50000000%7C%7CcheckMonth%3A999~800000%7C%7CisManagerFee%3B%5B%22add%22%5D%7C%7CbuildingType%3B%5B%22%EB%B9%8C%EB%9D%BC%2F%EC%A3%BC%ED%83%9D%22%2C%22%EC%95%84%ED%8C%8C%ED%8A%B8%22%2C%22%EC%98%A4%ED%94%BC%EC%8A%A4%ED%85%94%22%5D%7C%7CcontractType%3B%5B%22%EC%9B%94%EC%84%B8%22%5D%7C%7CroomType%3B%5B%22%ED%88%AC%EB%A3%B8%22%2C%22%EC%93%B0%EB%A6%AC%EB%A3%B8%22%5D%7C%7CroomCount_etc%3B%5B%221%EC%B8%B5+~+5%EC%B8%B5%22%2C%226%EC%B8%B5+%EC%9D%B4%EC%83%81%22%5D%7C%7CrealSize%3B%5B%2211%ED%8F%89+%EC%9D%B4%EC%83%81%22%5D&pageSize=90&pageIndex=1
~~~
---
복원 방법에 사용한 값들(schem, netloc 등)은 공식 문서 참고 부탁드립니다!  
(<https://docs.python.org/ko/3/library/urllib.parse.html>)