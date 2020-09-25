# Python+Django dev config

## WINDOWS:

### Install Python dev env

1.install Python
download and unzip;
add E:\Python\Python36 to ENV PATH;
then we can use python 

2.install pip
download and unzip 
cd pathtp/pip
python setup.py install
add E:\Python\Python36\Scripts to ENV PATH
then we can use pip

3.Install Django
run: pip install Django
E:\Python>python -m django --version
2.0.5

4.create python django project 
E:\Python>django-admin startproject myweb

E:\Python>tree /f myweb
文件夹 PATH 列表
卷序列号为 00000029 6279:F267
E:\PYTHON\MYWEB
│  manage.py
│
└─myweb
        settings.py
        urls.py
        wsgi.py
        __init__.py

E:\Python>cd myweb
E:\Python\myweb>python manage.py runserver
Performing system checks...
System check identified no issues (0 silenced).

You have 14 unapplied migration(s). Your project may not work properly until you apply the migrations for app(s): admin, auth, contenttypes, sessions.
Run 'python manage.py migrate' to apply them.
May 31, 2018 - 10:43:35
Django version 2.0.5, using settings 'myweb.settings'
Starting development server at http://127.0.0.1:8000/
Quit the server with CTRL-BREAK.

### Config Eclipse to dev python + django

1.Install PyDev
online(not stable) by Install New Software with：python - http://pydev.org/updates
offline by download,unzip and move plugins and features to eclipse;
2.Eclipse -preference - configure: python Interpreter to path to python.exe;
3.create new:  PyDev Django Project
4.run as: PyDev Django

### Deploy Python(Django) Project

Win+Nginx: https://my.oschina.net/ranvane/blog/343770



## Linux：

```
wget https://bootstrap.pypa.io/get-pip.py
python get-pip.py
pip -V　　#查看pip版本

pip install Django
```

