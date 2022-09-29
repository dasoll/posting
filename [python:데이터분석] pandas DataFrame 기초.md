<!-- [python/데이터분석] pandas DataFrame 기초 -->

## DataFrame 이란?
DataFrame이란 pandas 데이터분석 라이브러리의 가장 기본적인 객체입니다.  
2차원의 데이터, 즉 테이블, 표와 같은 데이터를 다룰 수 있게 도와줍니다.  

## 만드는 방법
2차원 데이터가 있으면 만들 수 있습니다.  
흔히 list, array, dict 객체로 만들게 됩니다.  

## list에서 DataFrame

~~~python
import pandas as pd

tmp_list = [[1,2,3,4,5], [6,7,8,9,10]]

pd.DataFrame(tmp_list)
~~~
---

2차원의 list에서 바로 DataFrame으로 변환할 수 있습니다.  

## array에서 DataFrame

~~~python
import pandas as pd
import numpy as np

tmp_list = [[1,2,3,4,5], [6,7,8,9,10]]

tmp_array = np.array(tmp_list)

pd.DataFrame(tmp_array)
~~~
---

2차원의 array에서 변환할 수 있습니다.

## dict에서 DataFrame

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6], 'B' : [2,7], 'C' : [3,8], 'D' : [4,9], 'E' : [5,10]}

pd.DataFrame(tmp_dict)
~~~
---

dict(dictionary) 객체에서 변환할 수 있습니다.  
dict 객체를 사용하면 컬럼명도 지정할 수 있는 특정이 있습니다.