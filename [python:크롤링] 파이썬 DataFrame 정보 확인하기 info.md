<!-- [python/크롤링] 파이썬 DataFrame 정보 확인하기 info  -->

## 데이터 분석의 시작

데이터분석을 시작하면 Data를 가져오고 DataFrame을 만듭니다.  

<br>

그리고 데이터프레임의 기본적인 정보를 가장 먼저 확인합니다.

<br>

결측치가 있는지,  
총 데이터는 몇개인지,  
컬럼의 데이터는 무슨 타입인지,

## info

이러한 기본정보를 확인할 수 있는 함수가 info 함수입니다.

<br>

<div>

~~~python
import pandas as pd

df = pd.read_csv('./경기도_평택시_비전동_221013.csv', encoding='euc-kr')
df.info()

# <class 'pandas.core.frame.DataFrame'>
# RangeIndex: 698 entries, 0 to 697
# Data columns (total 9 columns):
#  #   Column              Non-Null Count  Dtype 
# ---  ------              --------------  ----- 
#  0   articleName         698 non-null    object
#  1   realEstateTypeName  698 non-null    object
#  2   tradeTypeName       698 non-null    object
#  3   floorInfo           698 non-null    object
#  4   dealOrWarrantPrc    698 non-null    object
#  5   areaName            698 non-null    object
#  6   area2               698 non-null    int64 
#  7   buildingName        698 non-null    object
#  8   cpPcArticleUrl      698 non-null    object
# dtypes: int64(1), object(8)
# memory usage: 49.2+ KB
~~~
---

</div>

<br>

네이버 부동산에서 매물을 크롤링한 데이터프레임을 확인해보았습니다.  

<br>

빈 값은 없고 area2 컬럼을 제외하고는 전부 object(string) 타입인 것을 확인할 수 있습니다.

<br>

항상 분석을 시작하기에 앞서 가장 먼저 하는 작업입니다.

<br>

이런 기본정보들을 꼼꼼히 확인하는 습관을 들이면 좋으니 해보시기 바랍니다!