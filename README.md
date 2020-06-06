# Star Social

Blog Website build with Django for all topics space!




![Alt text](./static/simplesocial/images/StarSocial.gif?raw=true "Preview")

# Deployed Site 
* [Star Social](http://samkuttenk2.pythonanywhere.com/)

# Technologies
* [Django](https://www.djangoproject.com/)
* [Python](https://www.python.org/)
* [MySQL](https://www.mysql.com/)




# Code Snippets
   My url patterns for the main application
```python
     
 urlpatterns = [
    url(r"^$", views.HomePage.as_view(), name="home"),
    url(r"^test/$", views.TestPage.as_view(), name="test"),
    url(r"^thanks/$", views.ThanksPage.as_view(), name="thanks"),
    url(r"^admin/", admin.site.urls),
    url(r"^accounts/", include("accounts.urls", namespace="accounts")),
    url(r"^accounts/", include("django.contrib.auth.urls")),
    url(r"^posts/", include("posts.urls", namespace="posts")),
    url(r"^groups/",include("groups.urls", namespace="groups")),
]
```
My models.py for User Groups
```python
class Group(models.Model):
    name = models.CharField(max_length=255, unique=True)
    slug = models.SlugField(allow_unicode=True, unique=True)
    description = models.TextField(blank=True, default='')
    description_html = models.TextField(editable=False, default='', blank=True)
    members = models.ManyToManyField(User,through="GroupMember")

    def __str__(self):
        return self.name

    def save(self, *args, **kwargs):
        self.slug = slugify(self.name)
        self.description_html = misaka.html(self.description)
        super().save(*args, **kwargs)

    def get_absolute_url(self):
        return reverse("groups:single", kwargs={"slug": self.slug})


    class Meta:
        ordering = ["name"]


class GroupMember(models.Model):
    group = models.ForeignKey(Group, related_name="memberships", on_delete="models.Model")
    user = models.ForeignKey(User,related_name='user_groups', on_delete="models.Model")

    def __str__(self):

        return self.user.username

    class Meta:
        unique_together = ("group", "user")

```
    

# Author
  Sam Kuttenkuler
    - [Github](https://www.github.com/skuttenkuler)
    - [LinkedIn](https://www.linkedin.com/in/skdev91)
