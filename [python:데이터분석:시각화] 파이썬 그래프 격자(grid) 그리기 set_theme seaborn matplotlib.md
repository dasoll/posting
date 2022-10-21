<!-- [python/데이터분석/시각화] 파이썬 그래프 격자(grid) 그리기 set_theme seaborn matplotlib -->

## 그래프에서 격자 그리기

파이썬에서 그래프를 그리면 기본적으로 격자가 나오지 않습니다.

<br>

격자가 있으면 퀄리티가 확 높아지는 경우가 있기 때문에

<br>

격자를 만드는 방법을 알아보겠습니다.

## set_style

seaborn 패키지에서 제공하는 set_style 함수를 사용하면 됩니다.

<br>

<div>

~~~python
from sklearn.datasets import load_iris
import pandas as pd
import seaborn as sns
import matplotlib.pyplot as plt

iris = load_iris()
X = pd.DataFrame(iris.data, columns=iris.feature_names)
y = iris.target

sns.set_style('whitegrid')
sns.scatterplot(X.iloc[:, 0], y)
~~~
---
</div>

<br>

***whitegrid***, ***darkgrid*** 등의 스타일이 있습니다.

<br>

자세한 내용은 seaborn 공식 사이트에서 확인하실 수 있습니다.  
[Seaborn figure styles](https://seaborn.pydata.org/tutorial/aesthetics.html#:~:text=the%20matplotlib%20defaults.-,Seaborn%20figure%20styles,-%23)

<br>

**[스타일 적용 전]**

<img src="https://github.com/dasoll/posting/blob/main/image/%5Bpython:%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B6%84%EC%84%9D:%EC%8B%9C%EA%B0%81%ED%99%94%5D%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%20%EA%B7%B8%EB%9E%98%ED%94%84%20%EA%B2%A9%EC%9E%90(grid)%20%EA%B7%B8%EB%A6%AC%EA%B8%B0%20set_theme%20seaborn%20matplotlib_2.png?raw=true" width=500 />

<br>

<br>

**[스타일 적용 후]**

<img src="https://github.com/dasoll/posting/blob/main/image/%5Bpython:%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B6%84%EC%84%9D:%EC%8B%9C%EA%B0%81%ED%99%94%5D%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%20%EA%B7%B8%EB%9E%98%ED%94%84%20%EA%B2%A9%EC%9E%90(grid)%20%EA%B7%B8%EB%A6%AC%EA%B8%B0%20set_theme%20seaborn%20matplotlib_1.png?raw=true" width=500 />

## style 원래대로 복구하기

seaborn의 스타일을 설정했는데

<br>

마음에 들지 않을 경우가 생깁니다.

<br>

그럴 때는 reset_orig 함수를 사용하면 됩니다.

<br>

<div>

~~~python
import seaborn as sns

sns.reset_orig()
~~~
---

</div>

