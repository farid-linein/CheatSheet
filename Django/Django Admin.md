# Customizing how models are displayed

Now, we will take a look at how to customize the administration site. Edit the admin.py file of your blog application and change it, as follows.

```py
from django.contrib import admin
from .models import Post
@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'slug', 'author', 'publish', 'status']
```

We are telling the Django administration site that the model is registered in the site using a custom  class that inherits from ModelAdmin. In this class, we can include information about how to display  the model on the site and how to interact with it.  The list_display attribute allows you to set the fields of your model that you want to display on the  administration object list page. The @admin.register() decorator performs the same function as the  admin.site.register() function that you replaced, registering the ModelAdmin class that it decorates.  Let’s customize the admin model with some more options. Edit the admin.py file of your blog application and change it, as follows.

```py
from django.contrib import admin
from .models import Post
@admin.register(Post)
class PostAdmin(admin.ModelAdmin):
    list_display = ['title', 'slug', 'author', 'publish', 'status']
    list_filter = ['status', 'created', 'publish', 'author']
    search_fields = ['title', 'body']
    prepopulated_fields = {'slug': ('title',)}
    raw_id_fields = ['author']
    date_hierarchy = 'publish'
    ordering = ['status', 'publish']
```

 the author field is now displayed with a lookup widget, which can be much better than a dropdown

 select input when you have thousands of users. This is achieved with the raw_id_fields attribute
