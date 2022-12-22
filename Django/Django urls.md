# Form

**Creating forms with Django**

Django comes with two base classes to build forms:  

- Form: Allows you to build standard forms by defining fields and validations.  

- ModelForm: Allows you to build forms tied to model instances. It provides all the functionalities  of the base Form class, but form fields can be explicitly declared, or automatically generated, from model fields. The form can be used to create or edit model instances.

```py
from django import forms

class EmailPostForm(forms.Form):        
      name = forms.CharField(max_length=25)
      email = forms.EmailField()
      to = forms.EmailField()
      comments = forms.CharField(required=False,
                                 widget=forms.Textarea)
```

form contains the following fields:  

- name: An instance of CharField with a maximum length of 25 characters. We will use it for the  name of the person sending the post.  

- email: An instance of EmailField. We will use the email of the person sending the post recommendation.  

- to: An instance of EmailField. We will use the email of the recipient, who will receive the email recommending the post recommendation.  

- comments: An instance of CharField. We will use it for comments to include in the post rec-ommendation email. We have made this field optional by setting required to False, and we  have specified a custom widget to render the field.

**Handling forms in views**

```py
from .forms import EmailPostForm

def post_share(request, post_id):    
   # Retrieve post by id
   post = get_object_or_404(Post, id=post_id, status=Post.Status.PUBLISHED)
   if request.method == 'POST':
      # Form was submitted
      form = EmailPostForm(request.POST)
      if form.is_valid():
         # Form fields passed validation
         cd = form.cleaned_data
         # ... send email
   else:
      form = EmailPostForm()
   return render(request, 'blog/post/share.html', {'post': post,
                                                   'form': form})
```
