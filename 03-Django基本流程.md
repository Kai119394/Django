## Django基本流程

### 创建虚拟环境

* 安装虚拟环境:

  ```python
  pip install virtualenv
  # 查看是否安装成功
  virtualenv
  ```

* 新建文件夹存储虚拟环境

* 创建虚拟环境：

  ```python
  virtualenv --no-site-packages + 文件名
  ```

* 注意！使用下面命令可以不用安装virtualenv！

  ```python
  python -m venv + 文件名
  ```

###创建工程及app

* 进入虚拟环境：

  ```python
  cd Scripts
  activate
  # deactivate
  ```

* 安装django：

  ```python
  pip install django==1.11
  ```

* 创建工程

  ```python
  django-admin startproject project
  # project为工程名
  ```

* 创建应用

  ```python
  # 进入工程目录
  cd project
  python manae.py startapp app
  # app为应用名
  ```

###激活项目

* 使用pycharm打开工程

* 添加虚拟环境：

  File——setting——Project——Project Interpreter——Add Local——Existing environment——Scripts

* 配置Debug:

  Run——Debug——'+'——Python——manage.py——runserver 8080

* 修改setting.py文件

  ```python
  INSTALLED_APPS = [
      'django.contrib.admin',
      'django.contrib.auth',
      'django.contrib.contenttypes',
      'django.contrib.sessions',
      'django.contrib.messages',
      'django.contrib.staticfiles',
      'app'
  ]
  # 添加app
  ```

* 运行工程

  ```python
  python manage.py runserver
  # 默认端口号8000，后面可以接自定义端口号
  # python manage.py runserver 8080
  ```

### 配置数据库

#### 修改\__int__.py文件

```python
import pymysql

pymysql.install_as_MySQLdb()
```

#### 修改setting.py文件

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'aixf',
        'USER': 'root',
        'PASSWORD': '123456',
        'HOST': 'localhost',
        'POST': 3306
    }
}
```

### 创建模型类

####在应用目录下的models.py文件中

```python
from django.db import models


class Grades(models.Model):
    gname = models.CharField(max_length=20)
    gdate = models.DateTimeField()
    gboynum = models.IntegerField()
    ggirlnum = models.IntegerField()
    isDelete = models.BooleanField(default=False)
	
    # 自定义表名
    class Meta:
        db_table = 'grades'


class Students(models.Model):
    sname = models.CharField(max_length=20)
    sgender = models.BooleanField(default=True)
    sage = models.IntegerField
    scontend = models.CharField(max_length=20)
    isDelete = models.BooleanField(default=False)

    sgrade = models.ForeignKey('Grades')

    class Meta:
        db_table = 'students'
```

### 生成数据表

#### 生成迁移文件

```python
python manage.py makemigrations
```

#### 执行迁移

```python
python manage.py migrate
```

### 视图基本使用

#### 配置url

* 修改project目录下的urls.py文件

  ```python
  from django.conf.urls import url, include
  from django.contrib import admin
  
  urlpatterns = [
      url(r'^admin/', admin.site.urls),
      url(r'^app/', include('app.urls'))
  ]
  
  ```

* 在app应用目录下创建urls.py

  ```python
  from django.conf.urls import url
  from app import views
  
  urlpatterns = [
      url(r'^index/', views.index)
  ]
  ```

#### 定义视图

定义一个简单的视图

```python
from django.http import HttpResponse

def index(request):
    return HttpResponse('hello world!')
```

















### 