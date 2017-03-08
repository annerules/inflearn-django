# 기본 설정 및 프로젝트 초기화

## start project and app

## settings.py 수정
```python
INSTALLED_APPS = [
    'kilogram',
    #...

LANGUAGE_CODE = 'ko-kr'

TIME_ZONE = 'Asia/Seoul'

STATIC_ROOT = os.path.join(BASE_DIR, 'static')
```
## kilogram/urls.py 생성
```
from django.conf.urls import url
from . import views

app_name = 'kilogram'

urlpatterns = [
    url(r'^$', views.index, name = 'index'),
]
```
## mysite/urls.py 수정
```
from django.conf.urls import url, include
from django.contrib import admin
from kilogram import views as kilogram_views

urlpatterns = [
    url(r'^admin/', admin.site.urls),
    url(r'^$', kilogram_views.index, name = "root"),
    url(r'^kilogram/', include('kilogram_views.urls')),
]
```

## views.py 수정
```
def index(request):
    return render(request, "kilogram/index.html")
```

## 기본 템플릿 작성
- base.html
```html
<!DOCTYPE html>
<html lang="ko">
<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <!-- The above 3 meta tags *must* come first in the head; any other head content must come *after* these tags -->
  <title>Kilogram</title>

  <!-- Bootstrap -->
  <link href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">

  {% load static %}
  <link rel="stylesheet" type="text/css" href="{% static 'kilogram/style.css' %}" />

  <!-- HTML5 shim and Respond.js for IE8 support of HTML5 elements and media queries -->
  <!-- WARNING: Respond.js doesn't work if you view the page via file:// -->
  <!--[if lt IE 9]>
  <script src="https://oss.maxcdn.com/html5shiv/3.7.3/html5shiv.min.js"></script>
  <script src="https://oss.maxcdn.com/respond/1.4.2/respond.min.js"></script>
  <![endif]-->
</head>
<body>
  <nav class="navbar navbar-default navbar-static-top">
    <div class="container-fluid">
      <div class="navbar-header">
        <span class="navbar-brand glyphicon glyphicon-camera"></span>
      </div>
      <ul class="nav navbar-nav">
        <li><a href = "{% url 'kilogram:index' %}">Kilogram</a></li>
      </ul>
      <ul class="nav navbar-nav navbar-right">
        <li><a href = "{% url 'admin:index' %}">Admin</a></li>
      </ul>
    </div>
  </nav>
  <div class="container">
    <div>
      {% block content %}
      {% endblock %}
    </div>
  </div>
  <!-- jQuery (necessary for Bootstrap's JavaScript plugins) -->
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script>
  <!-- Include all compiled plugins (below), or include individual files as needed -->
  <script src="//maxcdn.bootstrapcdn.com/bootstrap/3.3.7/js/bootstrap.min.js"></script>
</body>
</html>

```
- index.html
```html
{% extends 'kilogram/base.html' %}
{% block content %}

<h1>Kilogram Main Page</h1>

{% endblock content %}
```