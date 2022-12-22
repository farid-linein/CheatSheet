```py
class PublishedManager(models.Manager):
    def get_queryset(self):
return super().get_queryset()\
.filter(status=Post.Status.PUBLISHED)
```
