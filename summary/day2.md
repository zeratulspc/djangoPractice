## 2일차
#### 모델 만들기

```python
from django.db import models

class ModelName(models.Model):
  foreign_key = models.ForeignKey()
  char_field = models.CharField(max_length=200)
  num_field = models.IntegerField()
  date_field = models.DateField()
```

위 코드와 같이 새로운 모델을 생성할수 있다 생성할수 있는 필드 종류에 대해 알고 싶으면 [여기](https://docs.djangoproject.com/en/3.2/ref/models/fields/#django.db.models.Field)를 읽어보자
