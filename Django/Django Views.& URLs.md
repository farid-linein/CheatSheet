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
