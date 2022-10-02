<!-- [python/크롤링] 파이썬 파일 이동하기 shutil move -->

## 파일 이동

파일을 드래그 & 드롭으로 이동시키거나 잘라내기 & 붙여넣기로 이동시킬 수 있습니다.
화면에서 이동하는 것처럼 python 코드 내에서 파일을 이동시킬 수도 있습니다.

## shutil

shutil의 move 함수를 이용하면 파일을 이동시킬 수 있습니다.

<br>

<div>

~~~python
import shutil

shutil.move('옮기고 싶은 파일 경로와 이름', '옮겨야할 파일 경로와 이름')
~~~
---

</div>

<br>

옮길 파일과 옮겨야할 위치와 파일명을 입력하면 옮길 수 있습니다.

## 예제

<div>

~~~python
import shutil

shutil.move(os.path.join('/Users/sorr/Downloads', 'DGS10.csv'), os.path.join('/Users/sorr/Documents/GitHub/study/economics/bond/data', 'DGS10.csv'))
~~~
---

</div>

<br>

예제에서 os.path.join 함수를 활용하여 경로와 파일명을 분리하여 입력했습니다.
경로가 다르고 파일명은 동일하다는 것을 직관적으로 확인할 수 있습니다.