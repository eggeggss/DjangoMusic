## DjangoMusic


<h2>1.安裝virtualenv</h2>
  
    pip install virtualenv --proxy auhqwsg01.corpnet.auo.com:8080
  
<h2>2.創建一個虛擬環境</h2>
  
    python -m virutalenv venv

<h2>3.啟動虛擬環境</h2>
  
    source activate

<h2>4.安裝django</h2>
  
    pip install django==1.11 --proxy auhqwsg01.corpnet.auo.com:8080

<h2>5.創建一個project</h2>

  django-admin startproject MyMusicProject

<h2>6.創建一個app</h2>

  python manage.py startapp ChineseApp
  
<h2>7.專案架構</h2>

![Alt Text](https://scontent.ftpe7-2.fna.fbcdn.net/v/t34.0-12/22052908_1873971256251290_2125481130_n.png?oh=1a5b0338b425f8d0d3448ac37fe5f947&oe=59CCB107)

<h2>9.設定專案路由</h2>
在urls.py中加入

<pre>
INSTALLED_APPS = [
    'ChineseApp.apps.ChineseAppConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
</pre>

<h2>8.在app下新增urls.py 並設定路由</h2>

<pre>
from django.conf.urls import url
from . import views

urlpatterns=[
    url(r'^$',views.index , name='index'),
    url(r'^/play/$',views.playmusic, name='playmusic'),
    url(r'^/returnlist/(?P<page_id>[0-9]+)$',views.returnlist,name='returnlist'),
]
</pre>

<h2>10.設定app路由</h2>

