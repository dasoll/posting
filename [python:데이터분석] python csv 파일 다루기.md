<!-- [python/데이터분석] python csv 파일 다루기 -->

## csv 파일
csv 파일은 comma-separated values의 약자입니다.  
해석해보면 콤마로 나뉜 값들인데 형태를 보면 왜 이름을 이렇게 지었는지 알 수 있습니다.  

<br>

A,B,C,D,E  
1,2,3,4,5

<br>

위와 같이 콤마로 연결해서 데이터를 표시하기 때문입니다.  

## csv 파일 불러오는 방법

pandas의 ***read_csv*** 함수를 이용해서 csv 파일을 불러올 수 있습니다.  

~~~python
import pandas as pd

pd.read_csv('./tmp.csv', encoding='euc-kr')
~~~
---

네이버 부동산 매물 포스팅에서 저장했던 csv 파일을 불러왔습니다.  
(참고 : [[python/크롤링] 네이버 부동산 아파트 매물 크롤링 by requests](https://ssorr.tistory.com/18))  

<br>

한글 저장을 위해 euc-kr 인코딩으로 저장했기 때문에 불러올 때도 마찬가지로 encoding을 지정해줍니다.  
encoding 파라미터의 기본값(default)은 'utf-8' 입니다.

## index_col, header 파라미터

~~~python
import pandas as pd

pd.read_csv('./tmp.csv', encoding='euc-kr', index_col=0, header=None)
~~~
---

이 외에도 index_col, header 파라미터가 있습니다.  
index_col은 index로 지정하고 싶은 컬럼을 지정할 수 있습니다.  

<br>

header는 컬럼이 될 행을 고를 수 있습니다.  
만약, 첫번째 행을 컬럼으로 지정하고 싶지 않다면 None으로 지정합니다.  

## csv 파일 저장하는 방법

DataFrame에서 to_csv 함수를 이용합니다.  

~~~python
import pandas as pd

tmp_df = pd.read_csv('./tmp.csv', encoding='euc-kr')

tmp_df.to_csv('./tmp2.csv', index=False, sep='\t')
~~~
---

## index, sep 파라미터

index 파라미터는 index 컬럼을 만들지 설정할 수 있습니다.  
기본값이 True라서 그냥 저장하면 의미없는 숫자 인덱스 컬럼이 추가됩니다.  

<br>

sep 파라미터는 콤마를 다른 문자로 대체할 수 있습니다.  
위에서 사용한 \t(탭), ;, :, $ 등 마음대로 사용할 수 있습니다.  

## 왜 sep을 이용해서 콤마 말고 다른 문자를 사용할까?

데이터 내에 콤마가 있을 경우가 있기 때문입니다.  
콤마가 컬럼을 나눈 것인지 데이터에 포함된건지 컴퓨터는 구분할 수 없습니다.  