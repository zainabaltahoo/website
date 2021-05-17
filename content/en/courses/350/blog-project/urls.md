---
# Page title
title: URLs

# Title for the menu link if you wish to use a shorter link title, otherwise remove this option.
linktitle: URLs

# Date page published
date: 2021-03-23

# Academic page type (do not modify).
type: book

# Position of this page in the menu. Remove this option to sort alphabetically.
weight: 6

draft: True


---
{{% callout note %}}
Switch to branch **6-urls** from **malmarz/isom350-blog** github repo to see this step's implementation
{{% /callout %}}

Django URLs allow us to link paths in our web application to iew function. Users of our web application cannot use a view function if it is not linked to a path. For example, we mentioned from our [last exercise on view]({{< ref "views.md" >}}) that DetailedView will allow users of our applications to specify the post they want to view using the URL. The example we used is that if a user opens the path `/post/1`, then they can view the details of the first post. With url paths, we can tell django that the `/post/` path is used to open the detailed view.

The main urls.py path is the one found at `mysite/urls.py`. This file details what path exist in our application. It already includes information on the admin interface and we can tell that the path `/admin/` will be related to the admin interface. We will follow a Django convention in organizing the urls for our blog application by first creating a urls.py file in our blog app. So create the new `/blog/urls.py` and update it to look like this:

```python
from . import views #1
from django.urls import path  #2

urlpatterns = [ #3
    path('', views.PostListView.as_view(), name='home'), #4
    path('<slug:slug>/', views.PostDetailView.as_view(), name='post_detail'), #5
] #6
```

So let's explain what is happening here:
- **In line #1**, we are importing all the view functions we created from the previous step, because we want to link them to paths.
- **In line #2**, we are important the path function that we will use to link paths to view function as we shall see in lines #4 and #5
- **In line #3**, this is how Django take the paths. We must use the variable **urlspattens**, which is a global Django variable, and update it with the **list** patterns that we want use for the paths in our applications. 
- **In line #4**, this is the first path we want to create, Path is just a function that accepts 3 arguments, the first one is the path, here an empty path means if we just mention our `/blog/` path without any addition to it, the PostListView will be shown (This is the second argument). The final argument is just a unique name we give to this path to make it wasy for us to create link to this path.
- **In line #5**, this is the same as line 4. Notice, the path is now `<slug:slug>/`. The < > tag is used to tell Django that we are expecting a slug (a special string) here and we want to extract that slug from the path and create a variable named also slug with the contents of the path and send it to the view function. If we change it to something like `<int:sid>/` means to expect an integer and that we want to extract that integer from the path and send the value as a variable named sid to the view function. But since we are using. The following [section from Django's documentation on URLs](https://docs.djangoproject.com/en/3.1/topics/http/urls/#how-django-processes-a-request) should clarify how paths should be written.
- **In line #6**, remember this is a python list, we have to close the list with a bracket.

What does this file do? well, here we are telling Django if the user open the `/blog/` path without any additional text in the path then our web app would display a list of posts. If the user opens `/blog/title-of-post` then django would search for a post that has the slug **title-of-post** and display it. Remember, slugs are just special strings with no spaces. It is commonly used to make urls to blogposts meaningful. So `/blog/my-first-python-program` is clearly a post about programming as apposed to `/blog/1` which we cannot tell will be about what.

But we are not completly done yet, we must link this urls.py file in our blog app to the main **mysite/urls.py**. This is achieved by updating **mysite/urls.py** as follows:

```python
from django.contrib import admin
from django.urls import path, include # Added include

urlpatterns = [
    path('admin/', admin.site.urls),   
    path('blog/', include('blog.urls')), # Added this line
]
```

Notice we updated two lines. The first one in the import, we added the include function which will be used to fetch the url paths we created in **blog/urls.py**. The 2nd line we added is just a path function again, but with only two paramaters. The first one is `blog/`, here we are telling Django that all our blog paths will start with `blog/`. The second argument is the path to `blog/urls.py`, but we removed the .py part and replaced the / with .. So all the paths we defined in `blog/urls.py` are now included as part of our web application. So go ahead and run the development server and you will see a different screen show up:

{{< figure src="courses/350/urls1.png" caption="The Expect Error After Wiring URLs Correctly" >}}

Here Django is telling us that it cannot find anything to serve at / (known as the root path), because we only defined `admin/` and `blog/`. As a matter of fact, as part of Django's assistance, it is displaying the list of paths that are recognized in our web app and its already showing both `admin/` and `blog/`. Remember to use this information to understand what is happenning. So now add the path `/blog/` to the url of your web application. If everything is done correctly, you should see the following error:

{{< figure src="courses/350/urls2.png" caption="The Expect Templates Related Error" >}}

Here Django is telling us that it successfully ran the PostList view function we created but cannot find the template post_list.html. This will be the last remaining piece to complete the functionality of our web application in listing posts, which we will explain in the next section.

