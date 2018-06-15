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

Além da API fácil de usar da Cloudinary, o seu plano gratuito é bastante generoso.

![Planos Cloudinary](https://res.cloudinary.com/mulhergorila/image/upload/v1529013672/blog-images/cloudinary-plans.jpg){:class="img-responsive"}


> #### recursos / aplicações
----------------------------
+ Servir arquivos estáticos (imagens, CSS, JS)
+ Armazenar arquivos de mídias (imagens, vídeos, pdf... enviados pelos usuários)
+ Manipulação de imagens (Muito além de crop e resize. Reconhecimento facial, OCR..)


<br />
## Chega de enrolação e vamos ao código!


<br />
> ### Ambdev

Antes de mais nada, vamos criar um ambiente de desenvolvimento.
```
$ python3 -m venv venv
```


Ativando o ambiente virtual e fazendo atualização do instalador de pacotes do python.
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
```
> O ponto `.` é crucial porque ele informa ao script para instalar o Django no seu diretório atual (para o qual o ponto . é uma referência abreviada).


Agora iremos executar a migração, criar um usuário e rodar o nosso projeto localmente.
```
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

Depois de ter feito isso, adicione cloudinary e cloudinary_storage aos aplicativos instalados em seu `settings.py`. Se você for usar este pacote para arquivos estáticos e / ou de mídia, certifique-se de que cloudinary_storage esteja antes de django.contrib.staticfiles:

```python
INSTALLED_APPS = [
    # ...
    'cloudinary_storage',
    'django.contrib.staticfiles',
    'cloudinary',
    # ...
]
```
> O django-cloudinary-storage sobrescreve o comando collectstatic do Django. Se você for usá-lo apenas para arquivos de mídia, o django.contrib.staticfiles que deve ser o primeiro:


Ainda no settings.py vamos adicionar os dados do Cloudinary. Se ainda não criou uma conta, você pode fazer aqui: [Cloudinary](https://cloudinary.com/invites/lpov9zyyucivvxsnalc5/tzrbis3noqte5tk0ttmh){:target="_blank"}

Após criar sua conta, acesse o dashboard, copie suas credenciais e adione ao `settings.py`

![Cloudinary Dashboard](https://res.cloudinary.com/mulhergorila/image/upload/v1529013672/blog-images/cloudinary-dashboard.jpg){:class="img-responsive"}

```python
CLOUDINARY_STORAGE = {
    'CLOUD_NAME': 'cloud_name',
    'API_KEY': 'api_key',
    'API_SECRET': 'api_secret'
}
```


Ainda no `settings.py` iremos configurar as URLs para static e media.
```python
STATIC_URL = '/static/'
STATICFILES_STORAGE = 'cloudinary_storage.storage.StaticHashedCloudinaryStorage'

MEDIA_URL = '/media/'  # or any prefix you choose
DEFAULT_FILE_STORAGE = 'cloudinary_storage.storage.MediaCloudinaryStorage'
```

Pronto. Isso é tudo que você irá precisar configurar para começar a usar o Cloudinary para armazenar os arquivos de mídia e estáticos do seu projeto.

Para ter certeza que está tudo funcionando, vamos rodar o projeto localmente com o as seguintes configurações no `settings.py`

```python
DEBUG = False
ALLOWED_HOSTS = ['*']
```
> Quando rodamos o projeto com `DEBUG = True` o Django sempre vai buscar os arquivos locais.
**Lembrando que em produção nunca deve ser usado `DEBUG = True`**

Agora vamos rodar o `collectstatic`
```
$ python manage.py collectstatic
$ python manage.py runserver
```
Execute o comando `collectstatic` sempre que houver mudanças nos arquivos estáticos.

{Análise dos arquivos estáticos }

Por enquanto é isto. Em breve publicarei a segunda perte do tutorial `Preparando o projeto para deploy na Heroku`


<br />
> Referências
[Django Cloudinary Storage](https://github.com/klis87/django-cloudinary-storage){:target="_blank"}
[Integrando o Django com Cloudinary](http://pythonclub.com.br/integrando-django-com-cloudinary.html){:target="_blank"}
