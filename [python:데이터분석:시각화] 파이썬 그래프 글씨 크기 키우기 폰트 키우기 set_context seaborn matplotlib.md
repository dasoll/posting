<!-- [python/데이터분석/시각화] 파이썬 그래프 글씨 크기, 폰트 키우기 set_context seaborn matplotlib -->

## 그래프 글씨

파이썬에서 그래프의 글씨 크기를 키우기가 어렵습니다.

<br>

축, 범주, 제목 등 일일히 바꿔줘야하기 때문입니다.

<br>

각각 스타일링이 가능하다는 것이 장점이 될 수 있지만

<br>

생산성 측면에서 떨어질 수 있습니다.

## set_context

seaborn의 set_context 함수를 활용하면 한번에 글씨 크기를 바꿀 수 있습니다.

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

sns.set_context('talk')
sns.scatterplot(X.iloc[:, 0], y)
~~~
---

</div>

<br>

***talk***, ***poster*** 등으로 크기 종류를 정할 수 있습니다.

<br>

자세한 내용은 seaborn 공식 사이트에서 확인하실 수 있습니다.  
[Scaling plot elements](https://seaborn.pydata.org/tutorial/aesthetics.html#:~:text=%7D\)%0Asinplot\(\)-,Scaling%20plot%20elements,-%23)

<br>

**[context 적용 전]**

<img src="https://github.com/dasoll/posting/blob/main/image/%5Bpython:%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B6%84%EC%84%9D:%EC%8B%9C%EA%B0%81%ED%99%94%5D%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%20%EA%B7%B8%EB%9E%98%ED%94%84%20%EA%B2%A9%EC%9E%90(grid)%20%EA%B7%B8%EB%A6%AC%EA%B8%B0%20set_theme%20seaborn%20matplotlib_2.png?raw=true" width=500 />

<br>

<br>

**[context 적용 후]**

<img src="https://github.com/dasoll/posting/blob/main/image/%5Bpython:%EB%8D%B0%EC%9D%B4%ED%84%B0%EB%B6%84%EC%84%9D:%EC%8B%9C%EA%B0%81%ED%99%94%5D%20%ED%8C%8C%EC%9D%B4%EC%8D%AC%20%EA%B7%B8%EB%9E%98%ED%94%84%20%EA%B8%80%EC%94%A8%20%ED%81%AC%EA%B8%B0%20%ED%82%A4%EC%9A%B0%EA%B8%B0%20%ED%8F%B0%ED%8A%B8%20%ED%82%A4%EC%9A%B0%EA%B8%B0%20set_context%20seaborn%20matplotlib.png?raw=true" width=500 />

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

