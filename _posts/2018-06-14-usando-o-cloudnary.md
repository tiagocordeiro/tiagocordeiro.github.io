---
layout: post
title:  "[tutorial] Usando o Cloudinary como alternativa ao S3 da AWS"
date:   2018-06-14 05:00:01 -0300
category: Tutorial
---

### Ambiente Virtual
```
$ python3 -m venv venv
$ source venv/bin/activate
$ pip install --upgrade pip
```

### Instalando o Django
```
$ pip install django
```

### Criando o projeto
```
$ django-admin startproject [meu-projeto] . 
$ python manage.py migrate
$ python manage.py createsuperuser
$ python manage.py runserver
```
{Análise dos arquivos estáticos }

### Instalando o Cloudinary
```
$ pip install django-cloudinary-storage
```
#### Settings.py 
```
INSTALLED_APPS = [
    # ...
    'cloudinary_storage',
    'django.contrib.staticfiles',
    'cloudinary',
    # ...
]

CLOUDINARY_STORAGE = {
    'CLOUD_NAME': 'hj7j3bfel',
    'API_KEY': '762422337134644',
    'API_SECRET': '0kYk1XmvaStLq93O1QAmZMMvuIM'
}

STATIC_URL = '/static/'
STATICFILES_STORAGE = 'cloudinary_storage.storage.StaticHashedCloudinaryStorage'

MEDIA_URL = '/media/'  # or any prefix you choose
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'

DEBUG=False
ALLOWED_HOSTS = ['*']
$ python manage.py collectstatic
```