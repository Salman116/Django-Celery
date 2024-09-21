python -m venv venv
Activate venv
pip install Django django-cors-headers djangorestframework
django-admin startproject django_celery_project .
python manage.py startapp django_celery_app
Add yourappname,  rest_framework,  corsheaders  in installed app
add .gitignore file
python manage.py makemigrations
python manage.py migrate
python manage.py runserver