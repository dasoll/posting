<!-- [python/크롤링] KB 월간 통계 엑셀 파일 받기 by selenium (1)  -->

## KB 월간 통계 엑셀 파일
KB 부동산 사이트에서 제공하는 월간 통계 엑셀 파일이 있습니다.  
우리나라 부동산 자료 대부분의 원소스라고 볼 수 있고 많은 강의에서도 사용합니다.  
매주, 매달 나오는 데이터를 자동으로 업데이트 하기 위한 첫 걸음으로 엑셀 파일을 받아보겠습니다.  

## selenium으로 KB 월간 통계 사이트 접속
저번 시간에 배운대로 KB 월간 통계를 받을 수 있는 페이지를 실행시켜 보겠습니다.  

---
~~~python
url = "https://kbland.kr/webview.html#/main/statistics?blank=true"
browser = webdriver.Chrome('./chromedriver')
browser.get(url)

while(True):
    pass
~~~
---
코드가 종료되면 chrome 창이 자동으로 종료됩니다.  
따라서, 코드가 종료되지 않도록 while문을 활용해 막아주었습니다.  

## 설치 후 실행
---
~~~python
from selenium import webdriver

url = "https://naver.com"
browser = webdriver.Chrome('./chromedriver')
browser.get(url)
~~~
---
기본적으로 chromedriver를 이용해 시작하는 방식입니다.  
chromedriver 파일을 .py 파일과 동일한 위치에 옮겨두었기 때문에 경로를 "./chromedriver"로 지정하였습니다.

## FileNotFoundError: [Errno 2] No such file or directory: 'chromedriver'
---
~~~
Traceback (most recent call last):
  File "/opt/anaconda3/envs/py39_64/lib/python3.9/runpy.py", line 197, in _run_module_as_main
    return _run_code(code, main_globals, None,
  File "/opt/anaconda3/envs/py39_64/lib/python3.9/runpy.py", line 87, in _run_code
    exec(code, run_globals)
  File "/Users/dasolseo/.vscode/extensions/ms-python.python-2022.12.0/pythonFiles/lib/python/debugpy/adapter/../../debugpy/launcher/../../debugpy/__main__.py", line 39, in <module>
    cli.main()
  File "/Users/dasolseo/.vscode/extensions/ms-python.python-2022.12.0/pythonFiles/lib/python/debugpy/adapter/../../debugpy/launcher/../../debugpy/../debugpy/server/cli.py", line 430, in main
    run()
  File "/Users/dasolseo/.vscode/extensions/ms-python.python-2022.12.0/pythonFiles/lib/python/debugpy/adapter/../../debugpy/launcher/../../debugpy/../debugpy/server/cli.py", line 284, in run_file
    runpy.run_path(target, run_name="__main__")
  File "/Users/dasolseo/.vscode/extensions/ms-python.python-2022.12.0/pythonFiles/lib/python/debugpy/_vendored/pydevd/_pydevd_bundle/pydevd_runpy.py", line 321, in run_path
    return _run_module_code(code, init_globals, run_name,
  File "/Users/dasolseo/.vscode/extensions/ms-python.python-2022.12.0/pythonFiles/lib/python/debugpy/_vendored/pydevd/_pydevd_bundle/pydevd_runpy.py", line 135, in _run_module_code
    _run_code(code, mod_globals, init_globals,
  File "/Users/dasolseo/.vscode/extensions/ms-python.python-2022.12.0/pythonFiles/lib/python/debugpy/_vendored/pydevd/_pydevd_bundle/pydevd_runpy.py", line 124, in _run_code
    exec(code, run_globals)
  File "/Users/dasolseo/Documents/GitHub/study/크롤링/example.py", line 4, in <module>
    browser = webdriver.Chrome()
  File "/opt/anaconda3/envs/py39_64/lib/python3.9/site-packages/selenium/webdriver/chrome/webdriver.py", line 69, in __init__
    super().__init__(DesiredCapabilities.CHROME['browserName'], "goog",
  File "/opt/anaconda3/envs/py39_64/lib/python3.9/site-packages/selenium/webdriver/chromium/webdriver.py", line 89, in __init__
    self.service.start()
  File "/opt/anaconda3/envs/py39_64/lib/python3.9/site-packages/selenium/webdriver/common/service.py", line 81, in start
    raise WebDriverException(
selenium.common.exceptions.WebDriverException: Message: 'chromedriver' executable needs to be in PATH. Please see https://chromedriver.chromium.org/home
~~~
---
위와 같은 에러가 발생하면 chromedriver를 다운로드 받아야 합니다.  
에러 마지막의 사이트에 가서 다운받을 수 있습니다.  
(<https://chromedriver.chromium.org/home>)  