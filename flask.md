Flask
=====

* 2004년 오스트리아의 오픈소스 개발자 아르민 로나허(Armin Ronacher)가 만든 웹 프레임워크<br>
~~만우절에 장난삼아 던진 아이디어였는데 서비스로 만들어졌다~~<br>

마이크로 웹 프레임워크다
---
여기서 마이크로란 뜻은. 기능이 부족해서가 아니라 **간결하게 유지하고 확장**할 수 있어서이다.

**그렇다면 확장이 자유롭다는 뜻이란 뭘까?**<br>
플라스크는 form, 즉 데이터베이스를 처리하는 기능이 없다.
(이를 지원하는 장고와 비교된다) 그러나 이러한 기능을 지원하는 모듈을 불러와 사용이 가능하다.
즉, 개발자가 원하는 기능을 필요한 만큼 가져다 쓸 수 있다.
## 문법
```python
# helloFlask.py

from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

if __name__ == "__main__":
    app.run()
```

위처럼 간결한 코드 몇줄로 웹 브라우저에 Hello world!를 띄울 수 있다.
이에 대한 간단한 문법 설명을 하자면.!

> **app = Flask(__name__)**<br>
>플라스크 애플리케이션을 생성하는 코드<br>
>__name__에는 모듈명이 담긴다<br>
>즉 파일이 실행되면(helloFlask.py)<br>
>__ name __ 변수에는 "helloFlask" 문자열이 선언된다


>**@app.route()**
URL과 플라스크 코드를 매핑하는 플라스크의 데코레이터다.<br>
즉 URL이 요청되면 그에 해당하는 함수를 실행한다.

간단한 문법을 설명했으니
이제 이걸 서버로 실행하는 방법을 알아보겠다<br>
## 실행
솔직히 가상환경 만드는거(python -m venv)는 귀찮으니 넘기고
이 가상환경을 활성화해서(Activate.ps1) pip install flask 하면 준비 끝인줄 알았는데<br>

<pre>
(example) PS C:\Develop\ShinMyeong-seop> flask run
Usage: flask run [OPTIONS]
Try 'flask run --help' for help.

Error: Could not locate a Flask application. Use the 'flask --app' option, 'FLASK_APP' environment variable, or a 'wsgi.py' or 'app.py' file in the current directory.
</pre>
이딴 오류가 뜨는것이다!
검색해보니 Flask를 사용하려면 환경변수를 잡아줘야 한단다 ㅋㅋ<br>

플라스크는 기본적으로 **app.py파일을 기본 애플리케이션으로 인식**하기 때문에 위에서 만든 helloFlask.py를 실행하려면 다음과 같은 절차를 밟아야 한다.

### 애플리케이션 설정하기

디렉터리에서 
<span style="color:#ffd33d">set FLASK_APP=helloFlask</span>명령을 실행하여 환경 변수 FLASK_APP에 helloFlask 값을 설정하자. 환경 변수에 설정한 helloFlask는 위에서 작성한 helloFlask.py 파일을 의미한다.

### 개발 서버를 디버깅 가능하도록 하기

디버그 모드는 오류가 발생하면 디버깅 결과 메시지를 웹 브라우저에 출력해 준다. 또한 서버 실행중에 프로그램을 변경하면 서버가 자동으로 다시 시작하여 변경된 내용을 적용해 준다.<br> 이도 
디렉터리에서 
<span style="color:#ffd33d">set FLASK_DEBUG=true</span>명령을 실행하면 된다.

하지만 매번 환경변수를 설정하고 디버깅 모드를 키는건 너무 귀찮으니<br>
myproject.cmd 파일에 이 명령들을 미리 추가하면 된다.    
[파일명: C:/venvs/myproject.cmd]

<pre>
@echo off
cd c:/projects/myproject
set FLASK_APP=파일이름
set FLASK_DEBUG=true
c:/venvs/myproject/scripts/activate
</pre>

~~근데 그냥 app.py 쓰면 되는거 아님?~~