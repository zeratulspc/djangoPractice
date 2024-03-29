## 1일차
#### 장고 프로젝트 파일 구조
- manage.py : 장고 커맨드라인 유틸리티
- djangoPractice/ : 프로젝트 디렉토리
- djangoPractice/&#95;&#95;init&#95;&#95;.py : 파이썬 **패키지 선언 파일**
- djangoPractice/settings.py : 프로젝트 **환경설정**
- djangoPractice/urls.py : url 선언, **라우팅**
- djangoPractice/asgi.py : *ASGI* 배포용 파일 <sub>(ASGI : 비동기 웹 서버와 애플리케이션을 위한 Python의 표준)</sub>
- djangoPractice/wsgi.py : *WSGI* 호환 웹서버 진입점 <sub>(WSGI:웹 서버 소프트웨어와 파이썬으로 작성된 웹 응용 프로그램 간의 표준 인터페이스)</sub>

#### 서버 실행 명령어

```
python manage.py runserver
```

#### URL 지정 관련 함수
**include()**

```python
include(module, namespace=None)
include(pattern_list)
include((pattern_list, app_namespace), namespace=None)
```

**path()**
```python
path(route, view, kwargs=None, name=None)
```

**URL 지정 예시**
```python
from django.contrib import admin
from django.urls import include, path

urlpatterns = [
    path('polls/', include('polls.urls')),
    path('admin/', admin.site.urls),
]
```
