# CUSTOM USER MODEL

```
always use a custom user model for all new Django projects. 
But the approach demonstrated in the official documentation 
example is actually not what many Django experts recommend. 
It uses the quite complex AbstractBaseUser when if we just use
AbstractUser instead things are far simpler and still customizable.
```

Creating our custom user model :

> • update settings.py  
> • create a new CustomUser model  
> • update the admin  
> • create new forms for UserCreationForm and UserChangeForm

```py
 INSTALLED_APPS = [  
'users.apps.UsersConfig', # new  
'django.contrib.admin',  
'django.contrib.auth',  
'django.contrib.contenttypes',  
'django.contrib.sessions',  
'django.contrib.messages',  
'django.contrib.staticfiles',  
]  
...  
AUTH_USER_MODEL = 'users.CustomUser' # new
```



Custom User Model

```py
# users/models.py

from django.contrib.auth.models import AbstractUser
from django.db import models


class CustomUser(AbstractUser):
    age = models.PositiveIntegerField(null=True, blank=True)

```

> **AbstractBaseUser vs AbstractUser**  
> AbstractBaseUser requires a very fine level of control and customization. We essentially rewrite Django. This can be helpful, but if we just want a custom user model  that can be updated with additional fields, the better choice is AbstractUser which  subclasses AbstractBaseUser. In other words, we write much less code and have less opportunity to mess things up. It’s the better choice unless you really know what  you’re doing with Django!
