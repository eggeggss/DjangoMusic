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

<h2>8.建立project 的 urls.py </h2>
<pre>
from django.conf.urls import url,include
from django.contrib import admin


urlpatterns = [
    url(r'^chineseapp',include('chineseapp.urls')),
    url(r'^admin/', admin.site.urls),
]
</pre>
<h2>9.在app下新增urls.py 並設定路由</h2>

<pre>
from django.conf.urls import url
from . import views
#index -> show hello
#play -> show 畫面
#returnlist ->web api
urlpatterns=[
    url(r'^$',views.index , name='index'),
    url(r'^/play/$',views.playmusic, name='playmusic'),
    url(r'^/returnlist/(?P<page_id>[0-9]+)$',views.returnlist,name='returnlist'),
]
</pre>

![alt tag](https://github.com/eggeggss/DjangoMusic/blob/master/螢幕快照%202018-12-01%20下午10.55.36.png?raw=true)


<h2>10.view.py</h2>

<pre>
from django.shortcuts import render
from django.http import HttpResponse
from django.template import loader
import json
from django.core.serializers import serialize

def index(request):

    return HttpResponse('Hello')


</pre>
<h2>11.runserver確認目前步驟無錯誤</h2>
    python manage.py runserver 0.0.0.0:8080

<h2>12.建Model</h2>
<pre>
from django.db import models
import json


class Music(models.Model):
      song_name=models.CharField(max_length=200)
      author_name=models.CharField(max_length=200)
      url=models.CharField(max_length=4096)
      img=models.CharField(max_length=4096,default="")
      page=models.IntegerField(default=0)
    
      def __str__(self):
          return self.song_name

    


</pre>

<h2>13.migrate model</h2>

1.python manage.py makemigrations chineseapp

2.python manage.py migrate

<h2>14.shell import </h2>
<pre>
python manage.py shell

from chineseapp.models import Music
m1=Music(song_name='多遠都要在一起',author_name='鄧紫棋',img='https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=afbb4e040846f21fdd395601974d0005/18d8bc3eb13533fafafa93d1aad3fd1f40345b84.jpg',page=1,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m1.save()

m2=Music(song_name='再見',author_name='鄧紫棋',img='https://gss1.bdstatic.com/-vo3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=11c989563a292df583cea447dd583705/b219ebc4b74543a90701b6b51e178a82b90114b4.jpg',page=1,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m2.save()

m3=Music(song_name='新的心跳',author_name='鄧紫棋',img='https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=97695c5695cad1c8c4b6f4751e570c6c/a8014c086e061d95ad5c7b417bf40ad162d9cab5.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m3.save()

m4=Music(song_name='來自天堂的魔鬼',author_name='鄧紫棋',img='https://gss0.bdstatic.com/94o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=d254fadab97eca80060831b5f04afcb8/d53f8794a4c27d1eb25e673d12d5ad6edcc438ca.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m4.save()

m5=Music(song_name='盲點',author_name='鄧紫棋',img='https://gss0.bdstatic.com/-4o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=ac54c65eab18972bb737089887a410ec/6a600c338744ebf8660e9e75d9f9d72a6059a779.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m5.save()

m6=Music(song_name='單行的軌道 ',author_name='鄧紫棋',img='https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=6a49a48d51da81cb5aeb8b9f330fbb73/91529822720e0cf310ed02820a46f21fbe09aab5.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m6.save()

m7=Music(song_name='一路逆風',author_name='鄧紫棋',img='https://gss1.bdstatic.com/-vo3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike116%2C5%2C5%2C116%2C38/sign=904f90e6f1deb48fef64a98c9176514c/810a19d8bc3eb1355e4fbd3ca41ea8d3fc1f44a8.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m7.save()

m8=Music(song_name='於是',author_name='鄧紫棋',img='https://gss0.bdstatic.com/-4o3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=00b4cae6329b033b3885f48874a75db6/d0c8a786c9177f3eb3972bef76cf3bc79e3d56b5.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m8.save()

m9=Music(song_name='瞬間',author_name='鄧紫棋',img='https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike80%2C5%2C5%2C80%2C26/sign=2cebbb689145d688b70fbaf6c5ab167b/b3fb43166d224f4acfb201480af790529822d146.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m9.save()

m10=Music(song_name='查克靠近 ',author_name='鄧紫棋',img='https://gss3.bdstatic.com/7Po3dSag_xI4khGkpoWK1HF6hhy/baike/c0%3Dbaike92%2C5%2C5%2C92%2C30/sign=9d7b88971d178a82da3177f2976a18e8/b17eca8065380cd78e7ed0b6a244ad345982810c.jpg',page=2,url='http://auomdm01.ddns.net/music/music00/01.mp3')
m10.save()
</pre>

<h2>14.setting.py</h2>
加入
<pre>
PROJECT_DIR = os.path.dirname(__file__)

STATIC_ROOT = os.path.join(PROJECT_DIR, 'static')

STATIC_URL = '/static/'

STATICFILES_DIRS = (
    ("js", os.path.join(STATIC_ROOT,'js')),
    ("css", os.path.join(STATIC_ROOT,'css')),
)
</pre>

<h2>15.目錄架構</h2>
project 下新增 static 下分別新增3目錄:css,js,json

<h2>16.css下新增 dropload.css</h2>
<pre>
.dropload-up,.dropload-down{
    position: relative;
    height: 0;
    overflow: hidden;
    font-size: 12px;
    /* 开启硬件加速 */
    -webkit-transform:translateZ(0);
    transform:translateZ(0);
}
.dropload-down{
    height: 50px;
}
.dropload-refresh,.dropload-update,.dropload-load,.dropload-noData{
    height: 50px;
    line-height: 50px;
    text-align: center;
}
.dropload-load .loading{
    display: inline-block;
    height: 15px;
    width: 15px;
    border-radius: 100%;
    margin: 6px;
    border: 2px solid #666;
    border-bottom-color: transparent;
    vertical-align: middle;
    -webkit-animation: rotate 0.75s linear infinite;
    animation: rotate 0.75s linear infinite;
}
@-webkit-keyframes rotate {
    0% {
        -webkit-transform: rotate(0deg);
    }
    50% {
        -webkit-transform: rotate(180deg);
    }
    100% {
        -webkit-transform: rotate(360deg);
    }
}
@keyframes rotate {
    0% {
        transform: rotate(0deg);
    }
    50% {
        transform: rotate(180deg);
    }
    100% {
        transform: rotate(360deg);
    }
}

</pre>

