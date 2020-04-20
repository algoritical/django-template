# Documentação {{cookiecutter.project_name}}

Esse projeto implementa o backend do projeto {{cookiecutter.project_name}}

## Instalação

- Faça o clone do projeto
```shell
git clone git@gitlab.com:{{cookiecutter.repo_name}}/{{cookiecutter.repo_name}}.git
```

- Instale as dependências
```shell
pipenv install
```

- Inicie os containers via docker-compose
```shell
docker-compose up -d
```

## Deploy

- Crie as instâncias de stagine e produção no Heroku
```shell
heroku create instance-staging --remote staging
heroku create instance --remote production
```

- Prepare os ambientes com os comandos abaixo, seguido de `-a <app-name>`
```shell
heroku config:set SECRET_KEY=`python contrib/secret_gen.py`
heroku config:set DEBUG=False
heroku config:set ALLOWED_HOSTS=.herokuapp.com

# Configure o email com sendgrid
heroku addons:create sendgrid:starter
heroku config:set EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
heroku config:set EMAIL_HOST_USER=`heroku config:get SENDGRID_USERNAME`
heroku config:set EMAIL_HOST_PASSWORD=`heroku config:get SENDGRID_PASSWORD`
```

## Comandos

* `make setup` - Configura o projeto para ambiente de desenvolvimento
* `make docs` - Iniciar servidor para visualizar documentação
* `make serve` - Inicia o servidor local
* `make migrate` - Executa as migrações
* `make makemigrations` - Cria novas migrações

## Layout do projeto

```
.
├── conftest.py
├── contrib
│   ├── env-sample
│   └── secret_gen.py
├── docker-compose.yml
├── docs
│   ├── docs
│   │   └── index.md
│   └── mkdocs.yml
├── manage.py
├── Pipfile
├── Pipfile.lock
├── {{cookiecutter.repo_name}}
│   ├── asgi.py
│   ├── core
│   │   ├── admin.py
│   │   ├── apps.py
│   │   ├── __init__.py
│   │   ├── managers.py
│   │   ├── migrations
│   │   ├── models.py
│   │   ├── tests
│   │   └── views.py
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
├── Procfile
├── pytest.ini
└── README.md
```

## Outras informações

Para entender melhor como funciona essa ferramenta de documentação, acesse [mkdocs.org](https://mkdocs.org).