# Django Views

### Using class-based views[¶](https://docs.djangoproject.com/en/4.1/topics/class-based-views/intro/#using-class-based-views "Permalink to this headline")

At its core, a class-based view allows you to respond to different HTTP request
methods with different class instance methods, instead of with conditionally
branching code inside a single view function.

So where the code to handle HTTP `GET` in a view function would look
something like:

![](C:\Users\Farid\AppData\Roaming\marktext\images\2022-08-14-19-19-57-image.png)

In a class-based view, this would become:

![](C:\Users\Farid\AppData\Roaming\marktext\images\2022-08-14-19-21-10-image.png)

When using Class-Based Views, you always add as_view() at the end of the view name.

> The major difference is that ListView is best to list items from a database called model, while TemplateView is best to render a template with no model. Both views can be very concise with different meaning. Below is sample of a list view in it simplest form
> 
> ```cpp
> Class SampleListView(ListView):    
>     model = ModelName
> ```
> 
> This will give you a context variable object_list and a template name in the form ("app_name/model_name_list.html") automatically that can be used to list all records in the database.
> 
> However, the TemplateView in its simplest form is
> 
> ```coffeescript
> class SampleTemplateView(TemplateView):
>     template_name = 'app_name/filename.html'
> ```

### URLS

```py
# pages_project/urls.py
from django.contrib import admin
from django.urls import path, include # new

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', include('pages.urls')), # new
]
```

```py
# pages/urls.py
from django.urls import path
from .views import HomePageView 

urlpatterns = [
    path('', HomePageView.as_view(), name='home'),
]
```

When using Class-Based Views, you always add as_view() at the end of the view name.

whene use, function-Base View

```py
from django.urls import path
from .views import homePageView

urlpatterns = [
    path('', homePageView, name='home')
]
```

### Extending Templates

The real power of templates is their ability to be extended. If you think about most web 
sites, there is content that is repeated on every page (header, footer, etc). Wouldn’t it 
be nice if we, as developers, could have one canonical place for our header code that 
would be inherited by all other templates?

```html
<!-- templates/base.html -->
<header>
<a href="{% url 'home' %}">Home</a> | <a href="{% url 'about' %}">About</a>
</header>
{% block content %}
{% endblock content %}
```

```html
<!-- templates/home.html -->
{% extends 'base.html' %}
{% block content %}
<h1>Homepage</h1>
{% endblock content %}
```

```html
<!-- templates/about.html -->
{% extends 'base.html' %}
{% block content %}
<h1>About page</h1>
{% endblock content %}
```

### Context object name

> At the top we specify that this template inherits from base.html. Then display the  title and body from our context object, which DetailView makes accessible as post. 
> 
> Personally I found the naming of context objects in generic views extremely confusing  when first learning Django. Because our context object from DetailView is either our  model name  **post**   or   **object**   we could also update our template as follows and it would work exactly the same.

```py
# blog/views.py
from django.shortcuts import render

from django.views.generic import ListView, DetailView
from .models import Post

# Create your views here.

class BlogListView(ListView):
    model = Post
    template_name = 'home.html'

class BlogDetailView(DetailView): # new
    model = Post
    # context_object_name = 'post_detail'
    template_name = 'post_detail.html'
```
