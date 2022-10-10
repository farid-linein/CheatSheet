# SETTING.PY config

## add new app

```py
INSTALLED_APPS = [
    'APP_NAME.apps.APP_NAMEConfig',
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
]
```

## Move Templates to Project Level

```py
TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.djanDjangoTemplates',
        # 'DIRS': [],
        'DIRS': [os.path.join(BASE_DIR, 'templates')],
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
```

Ketika merubah lokasi project templates ke Project Level

perlu mengimport OS

```py
import os

....code lainya
```

## Postgres DB

```py
DATABASES = {
   'default': {
       'ENGINE': 'django.db.backends.postgresql',
       'NAME': ‘<database_name>’,
       'USER': '<database_username>',
       'PASSWORD': '<password>',
       'HOST': '<database_hostname_or_ip>',
       'PORT': '<database_port>',
   }
}
```

##### example

```py
DATABASES = {
    'default': {
        # 'ENGINE': 'django.db.backends.sqlite3',
        # 'NAME': BASE_DIR / 'db.sqlite3',
        'ENGINE': 'django.db.backends.postgresql_psycopg2',
        'NAME': 'blog_db', 
        'USER': 'postgres', 
        'PASSWORD': 'admin',
        'HOST': '127.0.0.1', 
        'PORT': '5432',
    }
}
```
