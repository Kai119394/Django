### 创建项目
#### 配置虚拟环境（cmd命令提示符中执行）
1. pip install virtualenv  ——  安装虚拟环境
2. virtualenv  ——  查看虚拟环境是否安装
3. 新建文件夹存储虚拟环境
4. virtualenv --no-site-packages + 文件名  ——  创建虚拟环境
5. python -m venv + 文件名  —— 同上，创建虚拟环境
6. cd + 文件名
7. cd Scripts  ——  进入Scripts文件
8. avtivate  ——  启动虚拟环境
9. deactivate  —— 退出虚拟环境
10. pip install pymysql  ——  在虚拟环境中安装pymysql
11. pip install django==1.11  ——  在虚拟环境中安装Django（==后面接版本）
12. django-admin startproject + 项目名  ——  创建django项目
13. python manage.py startapp + 应用名  ——  创建app应用

#### 使用Pycharm打开项目
1. 目录层级说明
![这里写图片描述](https://img-blog.csdn.net/20180514212509774?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTc4MjA1MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

2. 在Pycharm中设置使用虚拟环境
  file — seeting — Project interpreter — Add local — Existing environment
3. 配置Debug运行模式
  Run—Debug—'+'—Python—runserver 8080
4. 设置setting配置文件
  LANGUAGE_CODE = 'zh-hans'  ——  设置中文
  TIME_ZONE = 'Asia/Shanghai'  ——  修改时区
  INSTALLED_APPS 中添加app名
5. python manage.py runserver  —— 启动项目(可以加端口号)
6. 网页显示
![这里写图片描述](https://img-blog.csdn.net/2018051423144462?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTc4MjA1MA==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
  
  