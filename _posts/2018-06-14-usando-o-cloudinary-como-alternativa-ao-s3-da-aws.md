---
layout: post
title:  "Usando o Cloudinary como alternativa ao S3 da AWS"
date:   2018-06-14 06:06:06 -0300
categories: 
    - "tutorial"
    - "django"
    - "cloudinary"
---


> Aprenda a criar um projeto Django, rodando na Heroku e integrado com Cloudinary

Gerenciar arquivos e imagens em produção pode ser um aborrecimento. Costuma ser bem difícil lidar com uploads, armazenamento, manipulação, administração e entrega de conteúdo de mídia em todos os projetos em que você começa ou está envolvido.

Felizmente, existem plataformas na nuvem que tiram o estresse de tudo isso, permitindo que você envie mais rapidamente e entregue seus produtos em grande escala. Cloudinary é uma dessas plataformas.


> #### recursos / aplicações
----------------------------
+ Servir arquivos estáticos (imagens, CSS, JS)
+ Armazenar arquivos de mídias (imagens, vídeos, pdf... enviados pelos usuários)
+ Manipulação de imagens (Muito além de crop e resize. Reconhecimento facial, OCR..)


Além da API fácil de usar da Cloudinary, o seu plano gratuito é bastante generoso.


<br />
> ### Ambdev

Vamos criar um ambiente virtual...
```
$ python3 -m venv venv
```


Ativando o ambiente virtual (upgrade pip)
```
$ source venv/bin/activate
(venv) $ pip install --upgrade pip
```


<br />
> ### Instalando o Django

```
(venv) $ pip install django
```


<br />
> ### Criando o projeto

```
(venv) $ django-admin startproject [meu-projeto] . 
(venv) $ python manage.py migrate
(venv) $ python manage.py createsuperuser
(venv) $ python manage.py runserver
```


{Análise dos arquivos estáticos }


<br />
> ### Cloudinary

```
(venv) $ pip install django-cloudinary-storage
```


<br />
> ### Ajustando o settings.py

```python
INSTALLED_APPS = [
    # ...
    'cloudinary_storage',
    'django.contrib.staticfiles',
    'cloudinary',
    # ...
]

CLOUDINARY_STORAGE = {
    'CLOUD_NAME': 'cloud_name',
    'API_KEY': 'api_key',
    'API_SECRET': 'api_secret'
}

STATIC_URL = '/static/'
STATICFILES_STORAGE = 'cloudinary_storage.storage.StaticHashedCloudinaryStorage'

MEDIA_URL = '/media/'  # or any prefix you choose
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'

DEBUG = False
ALLOWED_HOSTS = ['*']
```

```
$ python manage.py collectstatic
$ python manage.py runserver
```
{Análise dos arquivos estáticos }