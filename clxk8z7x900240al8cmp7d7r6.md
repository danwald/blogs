---
title: "Django soft delete Model using Managers"
datePublished: Tue Jun 18 2024 10:14:26 GMT+0000 (Coordinated Universal Time)
cuid: clxk8z7x900240al8cmp7d7r6
slug: django-soft-delete-model-using-managers
cover: https://cdn.hashnode.com/res/hashnode/image/stock/unsplash/HjBcAVWlxnE/upload/7b72745154edf93101cda85cb7b425b3.jpeg
tags: python, django, orm, delete

---

Below is the soft delete model you can inherit from. It uses an `active` field which on delete, it will only set to `False` and not actually delete the records from the overriden delete method. There is a provision available to actually delete records. It can be used in a cronjob to recover space etc.

```python
class SoftDeleteModel(models.Model):
    active = models.BooleanField(default=True, db_index=True)

    class Meta:
        abstract = True

    def delete(self, *args, **kwargs):  # pylint: disable=unused-argument
        if kwargs.pop('hard', False):
            return super().delete(*args, **kwargs)
        self.active = False
        self.save(update_fields=('active',))
        return (0, {self._meta.model_name: 0})
```

> One could use a `datetime` which indicates inactive records if set. It would also record the time when the delete occurred

The `ActiveQuerySet` overrides the `delete` method to allow for bulk delete. The corresponding manager uses the override so only active records are included. An `InactiveManage` which inherits from the default Manger is included for completeness.

```python
class ActiveQuerySet(models.QuerySet):
    def delete(self, *args, **kwargs):
        if kwargs.pop('hard', False):
            return super().delete(*args, **kwargs)
        return self.update(active=False)


class ActiveManager(models.Manager):
    def get_queryset(self):
        return ActiveQuerySet(self.model, using=self._db).exclude(active=False)

class InActiveManager(models.Manager):
    def get_queryset(self):
        return super().get_queryset().exclude(active=True)
```

Here's and example of it all put together.

```python
from django.db import models

class Textbooks(models.Model, SoftDeleteModel):
    id = models.UUIDField(db_index=True)
   
    objects = ActiveManager()
    deleted_objects = InActiveManager()
    all_objects = models.Manager()
```

> Notice that the default `objects` is overriden to only provide active records for all ORM actions.

### References

* [https://docs.djangoproject.com/en/5.0/topics/db/managers/](https://docs.djangoproject.com/en/5.0/topics/db/managers/)
    
* [https://medium.com/@akshatgadodia/chapter-8-extending-querysets-with-custom-methods-in-django-orm-d0b13f05408f](https://medium.com/@akshatgadodia/chapter-8-extending-querysets-with-custom-methods-in-django-orm-d0b13f05408f)