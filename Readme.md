http://13.209.64.249/blogs/post/

# 개발환경
- Django & sqlite
- AWS EC2
- nginx, gunicorn


# Tistory 블로그 구현

- Custom User model
  - AbstractUser를 사용

- 장고 내장모듈 Login, Logout
  - https://docs.djangoproject.com/en/1.10/topics/auth/default/#module-django.contrib.auth.views

- django-social-share
```
$ pip install django-social-share
```

```django
{% load social_share %}
{% block content %}
# ...........
# ...........
# ...........
# ...........
<button type="button" class="btn btn-light float-right">
  {% post_to_facebook post.get_absolute "facebook" %}
</button>
<button type="button" class="btn btn-light float-right">
  {% send_email post.title "New title: {{post.title}}. Check it out!" object_or_url "Share via email" %}
</button>
# ...........
# ...........
# ...........
{% endblock %}
```
- django-taggit

```
pip install django-taggit
```
```python
models.py
from django.db import models
from taggit.managers import TaggableManager

class Post(BaseModel):
    title = models.CharField(max_length=255, blank=False)
    content = models.TextField()
    tags = TaggableManager(
      verbose_name=_('tags'),
      help_text=_('A comma-separated list of tags.'),
      blank=True,
      through=TaggedPost,
    )

    def __str__(self):
        return '%s - %s' % (self.id, self.title)
```

- FBV(Function based view)
# reference
  - [Deploying Django Application To AWS EC2 instance](https://dev.to/subhamuralikrishna/deploying-django-application-to-aws-ec2-instance-2a81)