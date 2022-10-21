<!-- [python/통계/scipy] 파이썬 표본의 정규성 검정 (ks, shapiro, Lilliefors) -->

## 정규성과 등분산성

표본으로 모집단을 추정하기 위해서 필요한 가정이 있습니다.

<br>

그 중 표본이 정규분포 형태이고 두개의 집단일 경우 등분산성을 만족해야 합니다.

<br>

보통 공부하다보면 막연히 가정하는 경우가 있지만,

<br>

실제로 분석을 할 때는 표본이 정규성과 등분산성을 만족하는지 확인이 필요합니다.

<br>

참고로 검정하기 전에 이상치를 제거하고 해주는 것이 좋습니다.

## Kolmogorov Smirnov

Kolmogorov Smirnov 검정은 표본수가 많을 때 2개의 분포의 동질성을 확인하는 검정입니다. 

<br>

***귀무가설(H0)은 두 분포가 동일하다.***

<br>

즉, 정규분포를 따른다입니다.

<br>

<div>

~~~python
from scipy.stats import kstest, norm

my_data = norm.rvs(size=1000)
ks_statistic, p_value = kstest(my_data, 'norm')

print(ks_statistic, p_value)
# 0.03226916348924852 0.24390243627009853
~~~
---

</div>

<br>

p value가 0.244 정도로 0.05보다 크므로 귀무가설을 기각하지 못합니다. 

<br>

따라서, 표본이 정규분포를 따른다고 판단할 수 있습니다.

## Shapiro Wilk

Shapiro Wilk 검정은 표본 수가 많지 않을 때 (보통 50개 미만) 사용하는 검정입니다. 

<br>

Kolmogorov와 다르게 정규성 검정에서만 쓸 수 있습니다. 

<br>

마찬가지로 ***귀무가설은 정규분포를 따른다***입니다.

<br>

<div>

~~~python
from scipy.stats import norm, shapiro
my_data = norm.rvs(size=500)

print(shapiro(my_data))
#(0.9964019060134888, 0.3231377601623535)
~~~
---

</div>

<br>​

p value가 0.05보다 크므로 귀무가설을 기각하지 못합니다. 

<br>

따라서, 표본이 정규분포를 따른다고 판단할 수 있습니다.

## Lilliefors

Lilliefors 검정은 Kolmogorov 검정을 기반한 정규성 검정입니다. 

<br>

***귀무가설은 정규분포를 따른다입니다.***

​<br>

<div>

~~~python
from scipy.stats import norm
from statsmodels.stats.diagnostic import lilliefors

my_data = norm.rvs(size=500)

lilliefors(my_data)
# (0.026630724640602843, 0.6007178719186389)
~~~
---

</div>

<br>

p value가 0.05보다 크므로 귀무가설을 기각하지 못합니다. 

<br>

따라서, 표본이 정규분포를 따른다고 판단할 수 있습니다.