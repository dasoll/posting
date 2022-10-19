<!-- [python/데이터분석] 파이썬 통계량 평균 검정 t test  -->

## 평균 검정이란?

전통적인 통계적 방법으로 표본의 평균을 이용해 모집단의 평균을 추정하는 과정입니다.

<br>

모집단의 모수에 대한 가설을 세우고 (귀무 가설)

<br>

그 가정이 얼마나 맞는지 확률적으로 확인한 뒤

<br>

최종적으로 판단합니다.

## 판단 방법

유의 수준을 정한 뒤 (일반적으로 알파는 0.05)

<br>

계산되어 나온 결과 값의 p-value를 비교합니다.

<br>

p-value가 유의 수준보다 낮으면 가설을 기각합니다.  
(대립가설 채택)

## 단일 표본 (1 Sample) t-test

표본집단이 1개인 경우 일반적인 t test를 사용합니다.

<br>

<div>

~~~python
# 1 sample t-test
from scipy import stats

one_sample = [177.0, 182.7, 169.6, 176.8, 180.0]

result1 = stats.ttest_1samp(one_sample, popmean=177)
print(result1)

# Ttest_1sampResult(statistic=0.10039070766877535, pvalue=0.9248646407498543)
~~~
---

</div>

<br>

귀무가설은 "sample의 평균이 177"인 것이고

<br>

대립가설은 "sample의 평균이 177이 아니다"인 것입니다.

## 독립적인 두 표본 (Independent 2 Samples) t-test

표본 집단이 2개이지만 서로 독립일 경우 ttest_ind 함수를 사용합니다.

<br>

"귀무가설은 두 집단의 평균은 같다" 입니다.

<br>

<div>

~~~python
# independent t-test
from scipy import stats

male = [75, 85, 100, 72.5, 86.5]
female = [63.2, 76, 52, 100, 70]

two_sample = stats.ttest_ind(male, female)
print(two_sample)

# Ttest_indResult(statistic=1.233193127514512, pvalue=0.2525076844853278)
~~~
---

</div>

## 쌍으로 된 두 표본 (Paired 2 Samples) t-test

표본 집단이 2개이지만 서로 독립이 아닐 경우,

<br>

즉, 서로 연관이 되어있을 경우 ttest_rel 함수를 사용합니다.

<br>

"귀무가설은 두 집단의 평균은 같다" 입니다.

<br>

<div>

~~~python
# paired t-test
from scipy import stats

baseline = [67.2, 67.4, 71.5, 77.6, 86.0, 89.1, 59.5, 81.9, 105.5]
follow_up = [62.4, 64.6, 70.4, 62.6, 80.1, 73.2, 58.2, 71.0, 101.0]

paired_result = stats.ttest_rel(baseline, follow_up)
print(paired_result)

# Ttest_relResult(statistic=3.6681166519351103, pvalue=0.006326650855933662)
~~~
---

</div>