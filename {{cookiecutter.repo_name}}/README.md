# {{cookiecutter.repo_name}}

Backend of {{cookiecutter.repo_name}} project

## Install

- Clone the project
```shell
git clone git@gitlab.com:{{cookiecutter.group_name}}/{{cookiecutter.repo_name}}.git
```

- Install dependencies
```shell
pipenv install
```

- Start containers via docker-compose
```shell
docker-compose up -d
```

## Deploy

- Create instance
```shell
heroku create {{cookiecutter.repo_name}}-staging --remote staging
heroku create {{cookiecutter.repo_name}} --remote production
```

- Prepare environments
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

Para mais informações do projeto acesse a [documentação](https://{{cookiecutter.group_name}}.gitlab.io/{{cookiecutter.repo_name}})