### Creating a Model

### Syntax Model

```py
from django.db import models

class ModelName(models.Model):
        field_name = models.Field(**options)
```

### Example Models

```py
# import the standard Django Model
# from built-in library
from django.db import models

# declare a new model with a name "GeeksModel"
class GeeksModel(models.Model):
        # fields of the model
    title = models.CharField(max_length = 200)
    description = models.TextField()
    last_modified = models.DateTimeField(auto_now_add = True)
    img = models.ImageField(upload_to = "images/")

        # renames the instances of the model
        # with their title name
    def __str__(self):
        return self.title
```

### CLI

Whenever we create a Model, Delete a Model, or update anything in any
 of models.py of our project. We need to run two commands makemigrations
 and migrate. makemigrations basically generates the SQL commands for 
preinstalled apps (which can be viewed in installed apps in settings.py)
 and your newly created app’s model which you add in installed apps 
whereas migrate executes those SQL commands in the database file.   
So when we run,   
 

```
Python manage.py makemigrations
```

SQL Query to create above Model as a Table is created and   
 

```
 Python manage.py migrate
```

### Render a model in Django Admin Interface

from django.contrib import admin

# Register your models here.

```py
from .models import GeeksModel

admin.site.register(GeeksModel)
```

### Django CRUD – Inserting, Updating and Deleting Data

Django 
lets us interact with its database models, i.e. add, delete, modify and 
query objects, using a database-abstraction API called ORM(Object 
Relational Mapper). We can access the Django ORM by running the 
following command inside our project directory.  
 

python manage.py shell

**Adding objects**.   
To create an object of model Album and save it into the database, we need to write the following command:  
 

```
a = GeeksModel(
         title = "GeeksForGeeks",  
         description = "A description here",
         img = "geeks/abc.png"
         )
a.save()
```

**Retrieving objects**   
To retrieve all the objects of a model, we write the following command:  
 

```
GeeksModel.objects.all()
<QuerySet [<GeeksModel: Divide>, <GeeksModel: Abbey Road>, <GeeksModel: Revolver>]>
```

**Modifying existing objects**   
We can modify an existing object as follows:  
 

```
a = GeeksModel.objects.get(id = 3)
a.title = "Pop"
a.save()
```

**Deleting objects**   
To delete a single object, we need to write the following commands:  
 

```
a = Album.objects.get(id = 2)
a.delete()
```

To check detailed post of Django’s ORM (Object) visit [Django ORM – Inserting, Updating & Deleting Data](https://www.geeksforgeeks.org/django-orm-inserting-updating-deleting-data/)  
 

### Validation on Fields in a Model

Built-in
 Field Validations in Django models are the default validations that 
come predefined to all Django fields. Every field comes in with built-in
 validations from Django validators. For example, IntegerField comes 
with built-in validation that it can only store integer values and that 
too in a particular range.   
Enter the following code into models.py file of **geeks** app.   
 

```py
from django.db import models
from django.db.models import Model
# Create your models here.

class GeeksModel(Model):
    geeks_field = models.IntegerField()

    def __str__(self):
        return self.geeks_field
```

After running makemigrations and migrate on Django and rendering above model, let us try to create an instance using string “**GfG is Best**“.   
 

![built-in-validation-django-models](https://media.geeksforgeeks.org/wp-content/uploads/20191029155815/built-in-validation-django-models.png)

You
 can see in the admin interface, one can not enter a string in an 
IntegerField. Similarly every field has its own validations. To know 
more about validations visit, [Built-in Field Validations – Django Models](https://www.geeksforgeeks.org/built-in-field-validations-django-models/)

### More on Django Models –

- [Change Object Display Name using __str__ function – Django Models](https://www.geeksforgeeks.org/change-object-display-name-using-__str__-function-django-models-python/)   
   
- [Custom Field Validations in Django Models](https://geeksforgeeks.org/custom-field-validations-in-django-models/)
- [Django python manage.py migrate command](https://www.geeksforgeeks.org/django-manage-py-migrate-command-python/)
- [Django App Model – Python manage.py makemigrations command](https://www.geeksforgeeks.org/django-app-model-python-manage-py-makemigrations-command/)
- [Django model data types and fields list](https://write.geeksforgeeks.org/django-model-data-types-and-fields-list/)
- [How to use Django Field Choices ?](https://www.geeksforgeeks.org/how-to-use-django-field-choices/)
- [Overriding the save method – Django Models](https://www.geeksforgeeks.org/overriding-the-save-method-django-models/)

## Basic model data types and fields list

The
 most important part of a model and the only required part of a model is
 the list of database fields it defines. Fields are specified by class 
attributes. Here is a list of all Field types used in Django.   
 

| Field Name                                                                                          | Description                                                                                                                                                                 |
| --------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [AutoField](https://www.geeksforgeeks.org/autofield-django-models/)                                 | It An IntegerField that automatically increments.                                                                                                                           |
| [BigAutoField](https://www.geeksforgeeks.org/bigautofield-django-models/)                           | It is a 64-bit integer, much like an AutoField except that it is guaranteed to fit numbers from 1 to 9223372036854775807.                                                   |
| [BigIntegerField](https://www.geeksforgeeks.org/bigintegerfield-django-models/)                     | It<br> is a 64-bit integer, much like an IntegerField except that it is <br>guaranteed to fit numbers from -9223372036854775808 to <br>9223372036854775807.                 |
| [BinaryField](https://www.geeksforgeeks.org/binaryfield-django-models/)                             | A field to store raw binary data.                                                                                                                                           |
| [BooleanField](https://www.geeksforgeeks.org/booleanfield-django-models/)                           | A true/false field. <br>The default form widget for this field is a CheckboxInput.                                                                                          |
| [CharField](https://www.geeksforgeeks.org/charfield-django-models/)                                 | It is string filed for small to large-sized input                                                                                                                           |
| [DateField](https://www.geeksforgeeks.org/datefield-django-models/)                                 | A date, represented in Python by a datetime.date instance                                                                                                                   |
|                                                                                                     | It is used for date and time, represented in Python by a datetime.datetime instance.                                                                                        |
| [DecimalField](https://www.geeksforgeeks.org/decimalfield-django-models/)                           | It is a fixed-precision decimal number, represented in Python by a Decimal instance.                                                                                        |
| [DurationField](https://www.geeksforgeeks.org/durationfield-django-models/)                         | A field for storing periods of time.                                                                                                                                        |
| [EmailField](https://www.geeksforgeeks.org/emailfield-django-models/)                               | It is a CharField that checks that the value is a valid email address.                                                                                                      |
| [FileField](https://www.geeksforgeeks.org/filefield-django-models/)                                 | It is a file-upload field.                                                                                                                                                  |
| [FloatField](https://www.geeksforgeeks.org/floatfield-django-models/)                               | It is a floating-point number represented in Python by a float instance.                                                                                                    |
| [ImageField](https://www.geeksforgeeks.org/imagefield-django-models/)                               | It inherits all attributes and methods from FileField, but also validates that the uploaded object is a valid image.                                                        |
| [IntegerField](https://www.geeksforgeeks.org/integerfield-django-models/)                           | It is an integer field. Values from -2147483648 to 2147483647 are safe in all databases supported by Django.                                                                |
| [GenericIPAddressField](https://www.geeksforgeeks.org/genericipaddressfield-django-models/)         | An IPv4 or IPv6 address, in string format (e.g. 192.0.2.30 or 2a02:42fe::4).                                                                                                |
| [NullBooleanField](https://www.geeksforgeeks.org/nullbooleanfield-django-forms/)                    | Like a BooleanField, but allows NULL as one of the options.                                                                                                                 |
| [PositiveIntegerField](https://www.geeksforgeeks.org/positiveintegerfield-django-models/)           | Like an IntegerField, but must be either positive or zero (0).                                                                                                              |
| [PositiveSmallIntegerField](https://www.geeksforgeeks.org/positivesmallintegerfield-django-models/) | Like a PositiveIntegerField, but only allows values under a certain (database-dependent) point.                                                                             |
| [SlugField](https://www.geeksforgeeks.org/slugfield-django-models/)                                 | Slug<br> is a newspaper term. A slug is a short label for something, containing <br>only letters, numbers, underscores or hyphens. They’re generally used in<br> URLs.      |
| [SmallIntegerField](https://www.geeksforgeeks.org/smallintegerfield-django-models/)                 | It is like an IntegerField, but only allows values under a certain (database-dependent) point.                                                                              |
| [TextField](https://www.geeksforgeeks.org/textfield-django-models/)                                 | A large text field. The default form widget for this field is a Textarea.                                                                                                   |
| [TimeField](https://www.geeksforgeeks.org/timefield-django-models/)                                 | A time, represented in Python by a datetime.time instance.                                                                                                                  |
| [URLField](https://www.geeksforgeeks.org/urlfield-django-models/)                                   | A CharField for a URL, validated by URLValidator.                                                                                                                           |
| [UUIDField](https://www.geeksforgeeks.org/uuidfield-django-models/)                                 | A<br> field for storing universally unique identifiers. Uses Python’s UUID <br>class. When used on PostgreSQL, this stores in a uuid datatype, <br>otherwise in a char(32). |

#### Relationship Fields

Django also defines a set of fields that represent relations.

| Field Name                                                                                  | Description                                                                                                                                                                                                           |
| ------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [ForeignKey](https://www.geeksforgeeks.org/python-relational-fields-in-django-models/)      | A many-to-one relationship. Requires two positional arguments: the class to which the model is related and the on_delete option.                                                                                      |
| [ManyToManyField](https://www.geeksforgeeks.org/python-relational-fields-in-django-models/) | A<br> many-to-many relationship. Requires a positional argument: the class to<br> which the model is related, which works exactly the same as it does for<br> ForeignKey, including recursive and lazy relationships. |
| [OneToOneField](https://www.geeksforgeeks.org/python-relational-fields-in-django-models/)   | A<br> one-to-one relationship. Conceptually, this is similar to a ForeignKey <br>with unique=True, but the “reverse” side of the relation will directly <br>return a single object.                                   |

## Field Options

Field
 Options are the arguments given to each field for applying some 
constraint or imparting a particular characteristic to a particular 
Field. For example, adding an argument null = True to CharField will 
enable it to store empty values for that table in relational database.   
Here are the field options and attributes that an CharField can use.

| Field Options                                                                                    | Description                                                                                                                                                                                     |
| ------------------------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| [Null](https://www.geeksforgeeks.org/nulltrue-django-built-in-field-validation/)                 | If **True**, Django will store empty values as **NULL** in the database. Default is **False**.                                                                                                  |
| [Blank](https://www.geeksforgeeks.org/blanktrue-django-built-in-field-validation/)               | If **True**, the field is allowed to be blank. Default is **False**.                                                                                                                            |
| db_column                                                                                        | The name of the database column to use for this field. If this isn’t given, Django will use the field’s name. <br>                                                                              |
| [Default](https://www.geeksforgeeks.org/default-django-built-in-field-validation/)               | The<br> default value for the field. This can be a value or a callable object. <br>If callable it will be called every time a new object is created. <br>                                       |
| [help_text](https://www.geeksforgeeks.org/help_text-django-built-in-field-validation/)           | Extra “help” text to be displayed with the form widget. It’s useful for documentation even if your field isn’t used on a form. <br>                                                             |
| [primary_key](https://www.geeksforgeeks.org/primary_key-django-built-in-field-validation/)       | If True, this field is the primary key for the model.                                                                                                                                           |
| [editable](https://www.geeksforgeeks.org/editablefalse-django-built-in-field-validation/)        | If **False**,<br> the field will not be displayed in the admin or any other ModelForm. <br>They are also skipped during model validation. Default is **True**. <br>                             |
| [error_messages](https://www.geeksforgeeks.org/error_messages-django-built-in-field-validation/) | The<br> error_messages argument lets you override the default messages that the<br> field will raise. Pass in a dictionary with keys matching the error <br>messages you want to override. <br> |
| [help_text](https://www.geeksforgeeks.org/help_text-django-built-in-field-validation/)           | Extra “help” text to be displayed with the form widget. It’s useful for documentation even if your field isn’t used on a form. <br>                                                             |
| [verbose_name](https://www.geeksforgeeks.org/verbose_name-django-built-in-field-validation/)     | A<br> human-readable name for the field. If the verbose name isn’t given, <br>Django will automatically create it using the field’s attribute name, <br>converting underscores to spaces. <br>  |
| [validators](https://www.geeksforgeeks.org/custom-field-validations-in-django-models/)           | A list of validators to run for this field. See the [validators documentation](https://docs.djangoproject.com/en/2.2/ref/validators/) for more information. <br>                                |
| [Unique](https://www.geeksforgeeks.org/uniquetrue-django-built-in-field-validation/)             | If True, this field must be unique throughout the table. <br>                                                                                                                                   |



Context object name



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
