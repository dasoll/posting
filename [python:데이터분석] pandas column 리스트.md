<!-- [python/데이터분석] pandas DataFrame column list로 관리하기 -->
## 컬럼을 List로 관리하는 이유는?
컬럼을 list로 관리하는 가장 큰 이유는 컬럼별로 자료형이 다르기 때문입니다.    
***문자형과 숫자형은 전처리 과정에서 나눠서*** 처리해야하기 때문에 컬럼을 나눠서 관리하는 것이 필요합니다.   
데이터프레임 자체를 drop하고 merge 하면서 관리할 수 있지만 실수로 원본 데이터가 손상될 수 있습니다. 원본이 손상되면 매번 코드를 처음부터 다시 실행해서 복구해야 합니다.  
하지만, 컬럼을 list로 관리하게 되면 합치고 나누는 일이 수월하고 ***Feature Engineering을 하는데 유리***합니다.

## 컬럼 리스트 만들기
---
```python
col_train = train.columns.tolist()
train[col_train]
```
---
데이터프레임에서 columns를 호출하고 list로 바꿔줍니다.  
그리고 대괄호를 이용해 원하는 데이터를 출력합니다.  

## 타입별 컬럼 리스트 만들기
---
```python
col_object = train.select_dtypes('object').columns.tolist()
col_int = train.select_dtypes('int').columns.tolist()
col_float = train.select_dtypes('float').columns.tolist()
```
---
select_dtypes 메소드를 활용해 타입별로 컬럼 리스트를 만들 수 있습니다.  

## 컬럼 리스트 합치기
---
~~~python
col_numerical = col_int + col_float
~~~
---
리스트로 변환했을 때의 가장 큰 장점인 것 같습니다. 컬럼을 덧셈 연산으로 쉽게 더할 수 있습니다.

## 컬럼 리스트 빼기
---
~~~python
col_float = [col for col in col_numerical if col not in col_int]
~~~
---
하지만, 뺄셈 연산으로 뺄 수는 없고 for문을 통해 빼기 작업을 할 수 있습니다.  
python에서 자주 활용되는 ***for문과 if문의 조합***은 알아두시면 정말 좋습니다.