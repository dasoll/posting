<!-- [python/크롤링] selenium 설치 및 환경설정 -->

## selenium 설치하기
---
~~~
pip install selenium
~~~
---
위 명령어로 selenium을 설치할 수 있다.

## 설치 후 실행
---
~~~python
from selenium import webdriver

url = "https://naver.com"
browser = webdriver.Chrome('/Users/OOOOO/Documents/GitHub/study/크롤링/chromedriver')
browser.get(url)
~~~
---
기본적으로 chromedriver를 이용해 chrome을 실행시키는 방법입니다.시작하는 방식입니다.  
Chrome 메소드의 파라미터로 chromedriver 파일의 경로를 지정해줍니다.  

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