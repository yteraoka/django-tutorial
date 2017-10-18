# tutorial 1

https://docs.djangoproject.com/en/1.11/intro/tutorial01/

```
django-admin startproject mysite
```

これで mysite ディレクトリが作成される

さらに同名のサブディレクトリが作成され、全体の設定などがそこに置かれる

```
mysite/
├── manage.py
└── mysite
    ├── __init__.py
    ├── settings.py
    ├── urls.py
    └── wsgi.py
```

mysite ディレクトリの外は django の管理外である

manage.py はコマンドラインユーティリティで詳しくは
https://docs.djangoproject.com/en/1.11/ref/django-admin/
を読めと。

settings.py は設定ファイル
https://docs.djangoproject.com/en/1.11/topics/settings/

urls.py は url dispacher
https://docs.djangoproject.com/en/1.11/topics/http/urls/

wsgi.py は WSGI サーバーのエントリーポイント
https://docs.djangoproject.com/en/1.11/howto/deployment/wsgi/

## サーバーの起動

```
python manage.py runserver
```

で 127.0.0.1:8000 を Listen してサーバーが起動する

https://docs.djangoproject.com/en/1.11/ref/django-admin/#django-admin-runserver

## Polls アプリの作成

```
python manage.py startapp polls
```

```
polls
├── admin.py
├── apps.py
├── __init__.py
├── migrations
│   └── __init__.py
├── models.py
├── tests.py
└── views.py
```


# tutoriall 2

https://docs.djangoproject.com/en/1.11/intro/tutorial02/

## Database setup

デフォルトでは settings.py に次のように書いてあるため sqlite が使われる

```
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.sqlite3',
        'NAME': os.path.join(BASE_DIR, 'db.sqlite3'),
    }
}
```

```
python manage.py migrate
```

でマイグレーションが行われる

```
Operations to perform:
  Apply all migrations: admin, auth, contenttypes, sessions
Running migrations:
  Applying contenttypes.0001_initial... OK
  Applying auth.0001_initial... OK
  Applying admin.0001_initial... OK
  Applying admin.0002_logentry_remove_auto_add... OK
  Applying contenttypes.0002_remove_content_type_name... OK
  Applying auth.0002_alter_permission_name_max_length... OK
  Applying auth.0003_alter_user_email_max_length... OK
  Applying auth.0004_alter_user_username_opts... OK
  Applying auth.0005_alter_user_last_login_null... OK
  Applying auth.0006_require_contenttypes_0002... OK
  Applying auth.0007_alter_validators_add_error_messages... OK
  Applying auth.0008_alter_user_username_max_length... OK
  Applying sessions.0001_initial... OK
```

これは settings.py にデフォルトで 

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

とアプリが定義されているためにこれらのマイグレーションが実行された出力

```
python manage.py makemigrations polls
```

でマイグレーションファイルが作成される

```
python manage.py sqlmigrate polls 0001
```

とするとマイグレーション用 SQL が表示される

```
python manage.py sqlmigrate admin 0001
```


models.py を書く、settings.py に書く、
python manage.py makemigrations
を実行
python manage.py migrate
を実行


```
python manage.py shell
```

## Django Admin

```
python manage.py createsuperuser
```

`polls/admin.py` に admin 画面で操作したいモデルを追記する

```
from django.contrib import admin

from .models import Question

admin.site.register(Question)
```
