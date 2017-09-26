## DjangoMusic


1.安裝virtualenv
  
  pip install virtualenv --proxy auhqwsg01.corpnet.auo.com:8080
  
2.創建一個虛擬環境
  
  python -m virutalenv venv

3.啟動虛擬環境
  
  source activate

4.安裝django
  
  pip install django==1.11 --proxy auhqwsg01.corpnet.auo.com:8080

5.創建一個project

  django-admin startproject MyMusicProject

6.創建一個app

  python manage.py startapp ChineseApp
  
專案架構

 MusicProject
    |
    |
    ---- ChineseApp
    |         |
    |         ------admin.py
    |         |
    |         ------apps.py
    |         |
    |         ------models.py
    |         |
    |         ------views.py
    |
    -----MusicProject
    |         |
    |         ------setting.py
    |         |
    |         ------urls.py
    |         |
    |         ------wsgi.py
    |
    ----------manage.py



    

