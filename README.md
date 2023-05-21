# react-django
this is  a react-django project django
# Setting up the Django backend. 
mkdir React-Django
cd React-Django
# Create a Virtual environment. 
python3 -m venv env
source env/bin/activate
#install django
pip install django
django-admin startproject project1
cd project1
python manage.py migrate
python manage.py run server
# Setting up the react frontend. 
npx create-react-app frontend
cd frontend
npm start
# Interfacing the front end application to the Django backend. 
cd ..
edit the settings.py
import os
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [os.path.join(BASE_DIR, 'frontend', 'build')],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]
STATICFILES_DIRS = [os.path.join(BASE_DIR, 'frontend', 'build', 'static')]
python manage.py startapp core
edit views.py and add this
def front(request):
    context = { }
    return render(request, "index.html", context
 edit urls.py
 from django.contrib import admin
from django.urls import path
from core.views import front

urlpatterns = [
    path('admin/', admin.site.urls),
    path("", front, name="front"),
]

python manage.py runserver 
//Awesome the the integration is complete
