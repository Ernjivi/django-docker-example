# Django Docker

Dockerfile

Define una imagen: [Dockerfile reference](https://docs.docker.com/engine/reference/builder/), [Docker user guide](https://docs.docker.com/engine/tutorials/dockerimages/#building-an-image-from-a-dockerfile)

```
FROM python:3
ENV PYTHONUNBUFFERED 1
RUN mkdir /code
WORKDIR /code
COPY requirements.txt /code/
RUN pip install -r requirements.txt
COPY . /code/
```

requirements.txt

```
Django>=2.0,<3.0
psycopg2>=2.7,<3.0
```

docker-compose.yml

```yaml
version: '3'

services:
  db:
    image: postgres
  web:
    build: .
    command: python manage.py runserver 0.0.0.0:8000
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
```


## Creación del Proyecto

```
$ sudo docker-compose run web django-admin startproject composeexample .
```

## DB Config

```python
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': 'postgres',
        'USER': 'postgres',
        'HOST': 'db',
        'PORT': 5432,
    }
}
```

## Ejecutar docker-compose

```
$ docker-compose up
```


## Comandos útiles

```BASH
$ docker ps # Revisar dockers ejecutandose
$ docker exce -t -i <docker_id> bash # Ejecutar comandos en imagen
```

