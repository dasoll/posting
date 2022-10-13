<!-- [python/데이터분석] 파이썬 pandas DataFrame 순서로 선택하기 iloc -->

## loc에 이어서 iloc

저번 포스팅에 이어 iloc에 대해 알아보겠습니다.  
참고 : [[python/데이터분석] 파이썬 pandas DataFrame loc 함수](https://ssorr.tistory.com/33)

<br>

loc와 마찬가지로 행과 열을 지정해서 선택할 수 있습니다. 

<br>

“행”, “열” 순서로 입력해주고 loc와 다르게 이름이 아닌 행의 순서(index)를 입력해줍니다. 

<br>

순서는 0부터 시작한다는 점 꼭 기억해주시기 바랍니다.

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy)
display(df_copy.iloc[0, 2])
~~~
---

</div>

## 슬라이스 (slice)

마찬가지로 slice가 가능합니다. 

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy)
display(df_copy.iloc[1:2, 2:4])
~~~
---

</div>

<br>

iloc에서는 주의해야할 점이 앞의 숫자는 포함하고 뒤의 숫자는 포함하지 않습니다. 

<br>

즉 이상과 미만으로 slice가 됩니다.
 
<br>
 
1:2 행을 선택했기 때문에 앞에 1번 순서는 포함되고 뒤의 2번 순서는 포함되지 않았습니다. 

<br>

열도 2:4 열을 선택했기 때문에 2번 순서는 포함되고 4번 순서는 포함되지 않았습니다.
 
## list 활용, 데이터 일괄 변경

loc와 마찬가지로 모두 가능합니다.  

<br>

<div>

~~~python
import pandas as pd

tmp_dict = {'A' : [1,6,11], 'B' : [2,7,12], 'C' : [3,8,13], 'D' : [4,9,14], 'E' : [5,10,15]}

df = pd.DataFrame(tmp_dict)
df_copy = df.copy()

display(df_copy)
display(df_copy.iloc[0, 2])
~~~
---

</div>