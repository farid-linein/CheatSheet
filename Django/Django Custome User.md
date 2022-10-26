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
 """In practice, null and blank are commonly used together in this fashion so that a form
    allows an empty value and the database stores that value as NULL."""
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





# [How to add fields to the User model in Django](https://cpadiernos.github.io/how-to-add-fields-to-the-user-model-in-django.html "Permalink to How to add fields to the User model in Django")

Published: Wed 11 March 2020

By [Carol Padiernos](https://cpadiernos.github.io/author/carol-padiernos.html)

In [Django](https://cpadiernos.github.io/category/django.html).

tags: [Django](https://cpadiernos.github.io/tag/django.html)

This article assumes that you've done at least a beginner's tutorial on Django and you want to customize the built-in User model by adding more fields. These fields will be common among all the users. For example, if you want all users to have a "nickname" field, etc. I'll cover how to adjust your Admin views as well so that you can view, update, and add users with those added fields included.

## Setup

Create a project as you normally would:

`django-admin startproject myproject` 

---

**NOTE**

Do all the following steps BEFORE you do any 'python manage.py makemigrations' or 'python manage.py migrate'!

---

Create an application where you want to have your extended User model. In this case, we make an "accounts" application:

`cd myproject
python manage.py startapp accounts` 

## Models

Open your accounts models.py file, and add your User model. In our case, CustomUser:

`# models.py

from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    pass` 

## Settings

Add that app to myproject settings.py installed apps:

`# settings.py

INSTALLED_APPS = [
    ...
    ...
    'accounts', 
]` 

And then add to the bottom of the same file:

`# settings.py

AUTH_USER_MODEL = 'accounts.CustomUser'` 

---

**NOTE**

You can now run 'python manage.py makemigrations' and then 'python manage.py migrate' if you want to add fields later on.

---

## Models

To add fields to your model that you want to share among all the users, just include them in the CustomUser model. For example:

`# models.py

from django.contrib.auth.models import AbstractUser

class CustomUser(AbstractUser):
    is_student = models.BooleanField(default=False)
    is_teacher = models.BooleanField(default=False)
    mailing_address = models.CharField(max_length=200, blank=True)` 

## Admin

To be able to see the new CustomUser in the Admin site, you'll need to update your accounts application admin.py file:

`# admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    pass

admin.site.register(CustomUser, CustomUserAdmin)` 

---

**NOTE**

Don't forget to also 'python manage.py createsuperuser' so you can access the admin.

---

You'll notice that the user list view has the usual headings - email address, first name, last name, staff status.

## Admin list view

To add the fields as additional headings, you can use list_display:

`# admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    list_display = (
        'username', 'email', 'first_name', 'last_name', 'is_staff',
        'is_teacher', 'is_student', 'mailing_address'
        )

admin.site.register(CustomUser, CustomUserAdmin)` 

## Admin detail view

The user detail view will have username, password, first name, last name, email address, active, staff status, superuser status, groups, user permissions, last login, and date joined.

To add your new fields to the detail view, you'll need to use fieldsets. The below will emulate the original view with the new fields at the bottom.

`# admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    fieldsets = (
        (None, {
            'fields': ('username', 'password')
        }),
        ('Personal info', {
            'fields': ('first_name', 'last_name', 'email')
        }),
        ('Permissions', {
            'fields': (
                'is_active', 'is_staff', 'is_superuser',
                'groups', 'user_permissions'
                )
        }),
        ('Important dates', {
            'fields': ('last_login', 'date_joined')
        }),
        ('Additional info', {
            'fields': ('is_student', 'is_teacher', 'mailing_address')
        })
    )

admin.site.register(CustomUser, CustomUserAdmin)` 

## Admin add view

When you try to add a user, only username, password and password confirmation are available inputs. To have the new fields included as inputs, you can use add_fieldsets.

`# admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    add_fieldsets = (
        (None, {
            'fields': ('username', 'password1', 'password2')
        }),
        ('Personal info', {
            'fields': ('first_name', 'last_name', 'email')
        }),
        ('Permissions', {
            'fields': (
                'is_active', 'is_staff', 'is_superuser',
                'groups', 'user_permissions'
                )
        }),
        ('Important dates', {
            'fields': ('last_login', 'date_joined')
        }),
        ('Additional info', {
            'fields': ('is_student', 'is_teacher', 'mailing_address')
        })
    )

admin.site.register(CustomUser, CustomUserAdmin)` 

---

**NOTE**

Use "password1" and "password2" in "fields" to create and confirm the password.

---

## Admin complete

The complete admin file should look like this:

`# admin.py

from django.contrib import admin
from django.contrib.auth.admin import UserAdmin

from .models import CustomUser

class CustomUserAdmin(UserAdmin):
    list_display = (
        'username', 'email', 'first_name', 'last_name', 'is_staff',
        'is_teacher', 'is_student', 'mailing_address'
        )

    fieldsets = (
        (None, {
            'fields': ('username', 'password')
        }),
        ('Personal info', {
            'fields': ('first_name', 'last_name', 'email')
        }),
        ('Permissions', {
            'fields': (
                'is_active', 'is_staff', 'is_superuser',
                'groups', 'user_permissions'
                )
        }),
        ('Important dates', {
            'fields': ('last_login', 'date_joined')
        }),
        ('Additional info', {
            'fields': ('is_student', 'is_teacher', 'mailing_address')
        })
    )
    
    add_fieldsets = (
        (None, {
            'fields': ('username', 'password1', 'password2')
        }),
        ('Personal info', {
            'fields': ('first_name', 'last_name', 'email')
        }),
        ('Permissions', {
            'fields': (
                'is_active', 'is_staff', 'is_superuser',
                'groups', 'user_permissions'
                )
        }),
        ('Important dates', {
            'fields': ('last_login', 'date_joined')
        }),
        ('Additional info', {
            'fields': ('is_student', 'is_teacher', 'mailing_address')
        })
    )

admin.site.register(CustomUser, CustomUserAdmin)` 

Proudly powered by [Pelican](http://getpelican.com/), which takes great advantage of [Python](http://python.org/).
