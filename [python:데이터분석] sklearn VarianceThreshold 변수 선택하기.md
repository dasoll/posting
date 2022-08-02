<!-- [python/데이터분석] sklearn VarianceThreshold 변수 선택하기 -->
## 변수 선택이란?
학습할 데이터의 변수(feature)가 너무 많다보면 과적합(overfit)될 확률이 높고 예측 성능 또한 떨어질 수 있습니다. 그렇기 때문에 전처리 과정에서 변수를 줄이기 위해 다양한 방법을 사용합니다.  
그 중 분산이 0인 변수는 영향이 없다고 판단하고 제거해주어야 하는데 이것을 손쉽게 할 수 있게 도와주는 라이브러리가 바로 VarianceThreshold 입니다.  

## VarianceThreshold

### fit_transform
---
~~~python
from sklearn.feature_selection import VarianceThreshold
X = [[0, 2, 0, 3], 
     [0, 1, 4, 3], 
     [0, 1, 1, 3]]
selector = VarianceThreshold()
selector.fit_transform(X)
# array([[2, 0],
#        [1, 4],
#        [1, 1]])
~~~
---
먼저 sklearn.feature_selection 라이브러리에서 VarianceThreshold를 import 합니다.  
그리고 라이브러리를 호출한 후에 fit_transform으로 학습 후 변환해줍니다.  
대부분 전처리 라이브러리는 fit과 transform이 세트이기 때문에 알아두시면 좋습니다.  
결과를 보면 [0, 0, 0] 컬럼이 분산이 0이라서 제거된 것을 확인할 수 있습니다.

### get_support 
---
~~~python
import pandas as pd

mask = selector.get_support()
# array([False,  True,  True, False])

cols = pd.DataFrame(X).columns[mask]
pd.DataFrame(X)[cols]
#   1 2
# 0 2 0
# 1 1 4
# 2 1 1
~~~
---
get_support는 mask를 반환합니다.  
mask는 True, False 형태의 array로 boolean indexing을 통해 원하는 값을 뽑을 수 있게 도와줍니다.   결론적으로 컬럼 객체에 mask를 사용하면 0인 컬럼이 제거된 데이터를 구할 수 있습니다.  

### mask를 사용하는 이유
전처리를 할 때, 데이터프레임에서 컬럼을 직접 drop하지 않고 컬럼을 통해 컨트롤하기 위해 mask를 사용합니다. 물론 index를 통해 컨트롤 할 때도 사용됩니다.  
데이터프레임에서 직접 drop을 하다가 데이터가 손상되어 처음부터 다시 실행해야 되는 경우가 생길 수 있기 때문에 직접 drop보다는 mask와 컬럼을 통해 데이터를 컨트롤합니다.
