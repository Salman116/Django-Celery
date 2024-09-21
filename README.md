python -m venv venv
Activate venv
pip install Django django-cors-headers djangorestframework
django-admin startproject django_celery_project .
python manage.py startapp django_celery_app
Add yourappname,  rest_framework,  corsheaders  in INSTALLED_APPS
add .gitignore file
python manage.py makemigrations
python manage.py migrate
python manage.py runserver

# To include Celery
pip install celery redis  # make sure redis is installed in your machine also

# Create celery.py file in your project directory where settings.py file is
# Add these lines in it
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'django_celery_project.settings')

app = Celery('django_celery_project')

app.config_from_object('django.conf:settings', namespace='CELERY')

app.autodiscover_tasks()

# Add these lines in __init__.py file of same directory
from .celery import app as celery_app

__all__ = ('celery_app',)

# In settings.py add these lines
# Celery Settings
CELERY_BROKER_URL = 'redis://redis:6379/0'  # or your broker URL
CELERY_RESULT_BACKEND = 'redis://redis:6379/0'  # or your result backend
CELERY_ACCEPT_CONTENT = ['json']
CELERY_TASK_SERIALIZER = 'json'
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TIMEZONE = 'UTC'  # or your timezone

