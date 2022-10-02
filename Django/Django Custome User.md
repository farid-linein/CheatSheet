# CUSTOM USER MODEL

```
always use a custom user model for all new Django projects. 
But the approach demonstrated in the official documentation 
example is actually not what many Django experts recommend. 
It uses the quite complex AbstractBaseUser when if we just use
AbstractUser instead things are far simpler and still customizable.
```

## Creating our custom user model

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



For both new forms we are setting the model to our CustomUser and using the default fields via Meta.fields which includes all default fields. To add our custom age field we simply tack it on at the end and it will display automatically on our future sign up page. Pretty slick, no?

The concept of fields on a form can be confusing at first so let’s take a moment to explore it further. Our CustomUser model contains all the fields of the default User model and our additional age field which we set.

```python
# users/forms.py
from django import forms
from django.contrib.auth.forms import UserCreationForm, UserChangeForm

from .models import CustomUser

class CustomUserCreationForm(UserCreationForm):
    class Meta(UserCreationForm.Meta):
        model = CustomUser
        fields = UserCreationForm.Meta.fields + ('age',)

class CustomUserChangeForm(UserChangeForm):
    class Meta:
        model = CustomUser
        fields = UserChangeForm.Meta.fields
```



other step we need is to update our admin.py file since Admin is tightly  coupled to the default User model. We will extend the existing UserAdmin class to  use our new CustomUser model.

```py
# users/admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from form import CustomUserCreationForm, CustomUserChangeForm
from models import CustomUser

class CustomUserAdmin(UserAdmin):
    add_form = CustomUserCreationForm
    form = CustomUserChangeForm
    model = CustomUser

    
admin.site.register(CustomUser, CustomUserAdmin)
```
