## set up
1. set up environment
    - install python >3.6
    - install virtual env: 
    *python3 -m venv venv*
    *. venv/bin/activate*
2. set Django
    *pip install Django*
    
## Initiate 
 *django-admin startproject todoapp*

## run & test
 *cd todoapp*
 *python3 manage.py runserver*

## add seperate logic todolist
 *python manage.py startapp todolist*
 - todoapp/settings.py:
 ```python
 INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'todolist'
]
```

## add views
/todolist/views.py

## add urls for views
- create /todolist/urls.py
```python
from django.urls import path
from . import views
urlpatterns = [
    path('', views.index, name="index")
]
```
- adding paths to /todoapp/urls.py
```python
from django.urls import path, include
urlpatterns = [
    path('admin/', admin.site.urls),
    path('',include('todolist.urls'))
```

## Add templates
- add templates folder and file
- add "templates" to DIR in settings.py
```py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': ['templates'],
```

## Add models
implement todolist.models.py
```py
from django.db import models
# Create your models here.
class Todo(models.Model):
    title=models.CharField(max_length=350)
    complete=models.BooleanField(default=False)

    def __str__(self):
        return self.title
```
## Put togeter
*python manage.py makemigrations*
*python manage.py migrate*
*python manage.py createsuperuser*   ==> create a super user(admin)
(username: yangz, password: 52.....s...ly) to access admin panel: /admin

## Register the TODO model in admin.py
/todolist/admin.py
```admin.site.register(Todo)```

## Update views.py to use Todo Model
```py
from .models import Todo
# Create your views here.
def index(request):
    todos= Todo.objects.all()
    return render(request, "base.html",{"todo_list": todos})
```

## Summary
1. todoapp folder/todoapp
    settings.py: add todolist 
                 add templates
    urls.py: include all path of todolist
2. add templates folder
3. todolist : python manage.py startapp todolist
    models.py: add db model
    admin.py: register the model
    views.py: routes handler inside
    urls.py: adding all routes

