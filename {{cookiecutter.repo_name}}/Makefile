.PHONY: setup docs serve migrate makemigrations

setup:
	@pipenv install --dev

docs:
	@cd docs && mkdocs serve

serve:
	@python manage.py runserver 0.0.0.0:8000

migrate:
	@python manage.py migrate

makemigrations:
	@python manage.py makemigrations
