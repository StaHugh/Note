# Django 学习笔记
说明：
	参照官方文档，梳理学习思路

首先安装python，virtualenv,django.在虚拟环境中创建工程。
```
mysite/
    manage.py   ：工程命令工具，有兴趣阅读
    mysite/		：个人工程相关，是包名
        __init__.py ：空文件，告诉python这个目录是个包
        settings.py ：工程的设置
        urls.py
        wsgi.py   ：wsgi服务入口
```
**默认python3 manage.py ... 命令运行在manage.py所在目录**
运行命令：python3 manage.py runserver
----->因为没有配置提示  You have unapplied migrations
暂时不管提示，访问 127.0.0.1:8000 提示worked
改变端口：$ python manage.py runserver 8080
改变ip需要同时说明port：$ python manage.py runserver 0.0.0.0:8000
[参考runserver](https://docs.djangoproject.com/en/1.10/ref/django-admin/#django-admin-runserver)
代码修改会自动重新加载，但是添加文件就要重启服务器


## 现在工程建好了，可以开始新建app了。
project vs app:
app是web应用，实现某种功能，project是app和setting的集合。一个project可以包含多个app，一个app可以在多个project中。

新建投票应用：
$ python manage.py startapp polls
```
polls/
    __init__.py
    admin.py
    apps.py
    migrations/
        __init__.py
    models.py
    tests.py
    views.py
```
编写第一个view：
```
polls/views.py

from django.http import HttpResponse


def index(request):
    return HttpResponse("Hello, world. You're at the polls index.")


```
写好了一个view，要在网页上展示，就需要把这个view映射到一个url上，让人访问。因此我们需要配置urlconf。在polls目录下创建urls.py :
输入代码：
```
polls/urls.py

from django.conf.urls import url

from . import views

urlpatterns = [
    url(r'^$', views.index, name='index'),
]

```
然后在配置说明工程的URLConfig在urls.py中。

修改代码：（注意修改mysite中的urls.py）
```
mysite/urls.py

from django.conf.urls import include, url
from django.contrib import admin

urlpatterns = [
    url(r'^polls/', include('polls.urls')),
    url(r'^admin/', admin.site.urls),
]

```
include 函数允许你调用其他部分的URLConfs,include 函数不包含$(字符串结束符)，而是斜杠（/）。

启动服务：python3 manage.py runserver
就可以看到自己写的内容了。

讨论url()函数的参数：两个必须参数 regex  and view ;two optional args :kwargs and name .
