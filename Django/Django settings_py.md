# SETTING.PY config

### add new app

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

### Move Templates to Project Level

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
