# DjangoBlog

A blog system based on `python3.6` and `Django2.1`.

[![Build Status](https://travis-ci.org/liangliangyy/DjangoBlog.svg?branch=master)](https://travis-ci.org/liangliangyy/DjangoBlog) [![codecov](https://codecov.io/gh/liangliangyy/DjangoBlog/branch/master/graph/badge.svg)](https://codecov.io/gh/liangliangyy/DjangoBlog) [![Requirements Status](https://requires.io/github/liangliangyy/DjangoBlog/requirements.svg?branch=master)](https://requires.io/github/liangliangyy/DjangoBlog/requirements/?branch=master)  [![license](https://img.shields.io/github/license/liangliangyy/djangoblog.svg)]()  

## Main Features:
- Articles, Pages, Categories, Tags(Add, Delete, Edit), edc. Articles and pages support `Markdown` and highlighting.
- Articles support full-text search.
- Complete comment feature, include posting reply comment and email notification. `Markdown` supporting.
- Sidebar feature: new articles, most readings, tags, etc.
- OAuth Login supported, including Google, GitHub, Facebook, Weibo, QQ.
- `Memcache` supported, with cache auto refresh.
- Simple SEO Features, notify Google and Baidu when there was a new article or other things.
- Simple picture bed feature integrated.
- `django-compressor` integrated, auto-compressed `css`, `js`.
- Website exception email notification. When there is an unhandle exception, system will send an email notification.
- Wechat official account feature integrated. Now, you can use wechat official account to manage your VPS.

## Installation
Change MySQL client from `pymysql` to `mysqlclient`, more details please reference [pypi](https://pypi.org/project/mysqlclient/) , checkout preperation before installation.

Install via pip: `pip install -Ur requirements.txt`

If you do NOT have `pip`, please use the following methods to install:
- OS X / Linux, run the following commands: 

    ```
    curl http://peak.telecommunity.com/dist/ez_setup.py | python
    curl https://raw.github.com/pypa/pip/master/contrib/get-pip.py | python
    ```

- Windows：

    Download http://peak.telecommunity.com/dist/ez_setup.py and https://raw.github.com/pypa/pip/master/contrib/get-pip.py, and run with python. 

### Configuration
Most configurations are in `setting.py`, others are in backend configurations.

I set many `setting` configuration with my environment variables (such as: `SECRET_KEY`, `OAUTH`, `mysql` and some email configuration parts.) and they did NOT been submitted to the `GitHub`. You can change these in the code with your own configuration or just add them into your environment variables.

Files in `test` directory are for `travis` with automatic testing. You do not need to care about this. Or just use it, in this way to integrate `travis` for automatic testing.

In `bin` directory, we have scripts to deploy with `Nginx`+`Gunicorn`+`virtualenv`+`supervisor` on `linux` and `Nginx` configuration file. You can reference with my article

>[DjangoBlog部署教程](http://ee-fans.com)

More deploy detail in this article.

## Run

Modify `DjangoBlog/setting.py` with database settings, as following:

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.mysql',
        'NAME': 'djangoblog',
        'USER': 'root',
        'PASSWORD': 'password',
        'HOST': 'host',
        'PORT': 3306,
    }
}
```

### Create database
Run the following command in MySQL shell:
```sql
CREATE DATABASE `djangoblog` /*!40100 DEFAULT CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci */;
```

Run the following commands in Terminal:
```bash
./manage.py makemigrations
./manage.py migrate
```

**Attention: ** Before you using `./manage.py`, make sure the `python` command in your system is towards to `python 3.6` or above version. Otherwise you may solve this by one of the two following methods:
- Modify the first line in `manage.py`, change `#!/usr/bin/env python` to `#!/usr/bin/env python3`
- Just run with: `python3 ./manage.py makemigrations`

### Create super user

Run command in terminal:
```bash
./manage.py createsuperuser
```

### Create testing data
Run command in terminal:
```bash
./manage.py create_testdata
```

### Collect static files
Run command in terminal:
```bash
./manage.py collectstatic --noinput
./manage.py compress --force
```

### Getting start to run server
Execute: `./manage.py runserver`

Open up a browser and visit: http://127.0.0.1:8000/ , the you will see the blog.

## More configurations
[More configurations details](/docs/config-en.md)
