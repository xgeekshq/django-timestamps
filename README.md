# Django Timestamps

Timestamps and Soft Delete Patterns in Django Models.

1. Add "timestamps" to your INSTALLED_APPS setting like this:

```python
INSTALLED_APPS = [
    # ...
    'timestamps',
]
```

2. In your models:

a) For models you want timestamps, just inherit Timestample:

```python
from timestamps.models import models, Timestample


class YourModel(Timestample, models.Model):
    # your fields here ...

```

b) For models you want soft-delete, just inherit SoftDeletes:

```python
from timestamps.models import models, SoftDeletes


class YourModel(SoftDeletes, models.Model):
    # your fields here ...

```

c) If you want both, you can also inherit from Model for shorter convenience:

```python
from timestamps.models import models, Model


class YourModel(Model, models.Model):
    # your fields here ...

```


## Soft Deleting

- To get all objects without the deleted ones:

```python queryset = YourModel.objects```

- To get only deleted objects:

```python queryset = YourModel.objects_deleted```

- To get all the objects, including deleted ones:

```python queryset = YourModel.objects_with_deleted```


### To soft delete an instance

```python
some_model = MyModel.objects.first()
some_model.delete()  # or some_model.delete(hard=False)
```

### To restore an instance

```python
some_model = MyModel.objects_deleted.first()
some_model.restore()
```

### To hard delete an instance

```python
some_model = MyModel.objects.first()
some_model.delete(hard=True)
```

### To bulk soft delete a queryset

```python
qs = MyModel.objects  # you can also apply filters to bulk delete a subset: qs = MyModel.objects.filter(...)
qs.delete()  # or some_model.delete(hard=False)
```

### To bulk hard delete a queryset

```python
qs = MyModel.objects  # ... bulk hard delete a subset: qs = MyModel.objects.filter(...)
qs.delete(hard=True)
```

### To bulk restore a queryset

```python
qs = MyModel.objects_deleted  # ... bulk restore a subset: qs = MyModel.objects_deleted.filter(...)
qs.restore()  # or some_model.delete(hard=False)
```
