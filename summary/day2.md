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

위 코드와 같이 새로운 모델을 생성할수 있다,
생성할수 있는 필드 종류에 대해 알고 싶으면 [여기](https://docs.djangoproject.com/en/3.2/ref/models/fields/#django.db.models.Field)를 읽어보자

#### 모델의 활성화

생성한 모델을 활성화 하기 위해선 모델이 속해있는 앱이 프로젝트 설정 파일에 포함되어있어야함

```python
INSTALLED_APPS = [
    'polls.apps.PollsConfig', # 모델이 속해있는 앱을 프로젝트 설정 파일에 추가해준다
    ... 
]
```

프로젝트에 모델이 속해있는 앱이 포함되었다면 아래의 명령어를 입력한다

```
$ python manage.py makemigrations polls
```
결과 :
```
Migrations for 'polls':
  polls/migrations/0001_initial.py
    - Create model Question
    - Create model Choice
```

위의 과정을 통해서 마이그레이션 파일이 생성되었음.
마이그레이션 파일은 내가 사용하는 DB에 변경사항을 적용할때 사용할 수 있음

예시 :
```
$ python manage.py sqlmigrate polls 0001
```
결과 :
```sql
BEGIN;
--
-- Create model Question
--
CREATE TABLE "polls_question" (
    "id" serial NOT NULL PRIMARY KEY,
    "question_text" varchar(200) NOT NULL,
    "pub_date" timestamp with time zone NOT NULL
);
--
-- Create model Choice
--
CREATE TABLE "polls_choice" (
    "id" serial NOT NULL PRIMARY KEY,
    "choice_text" varchar(200) NOT NULL,
    "votes" integer NOT NULL,
    "question_id" integer NOT NULL
);
ALTER TABLE "polls_choice"
  ADD CONSTRAINT "polls_choice_question_id_c5b4b260_fk_polls_question_id"
    FOREIGN KEY ("question_id")
    REFERENCES "polls_question" ("id")
    DEFERRABLE INITIALLY DEFERRED;
CREATE INDEX "polls_choice_question_id_c5b4b260" ON "polls_choice" ("question_id");

COMMIT;
```

위와 같은 마이그레이션 파일을 통해 자동으로 생성된 명령어가 실행되면서 내 DB에 모델들의 변경사항이 적용됨.
