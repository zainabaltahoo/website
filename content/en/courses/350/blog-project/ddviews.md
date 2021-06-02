---
# Page title
title: Data-Driven Views

# Title for the menu link if you wish to use a shorter link title, otherwise remove this option.
linktitle: Data-Driven Views

# Date page published
date: 2021-03-23

# Academic page type (do not modify).
type: book

# Position of this page in the menu. Remove this option to sort alphabetically.
weight: 8

draft: false


---

Data-Driven views are just [regular views in Django]({{< ref "courses/350/blog-project/views.md" >}}), except that they use the model later to fetch/store data from the database.

With data-driven views, you take advantage of the Django ORM to build views that perform the basic CRUD operations:
  1. Fetch data **(Focus of this section)**
  2. Store data
  3. Update data
  4. Delete Data

In this section, our focus will be on building views that displays data (The fetch/read operation). In later sections, we will cover the other operations.

The fetch operation is necessary to read data from a database before it can be displayed on screen. Views that display data can be categorized into either views that display: 

- A list of objects (known as list views).
- details of a single object (known as detailed views).

A typical web application will display list of data (e.g., posts, products, students ...etc) and allow the user to filter, sort, or choose to display a single item in more detail. In our blog application, our goal is to display first a list of blog posts titles, where the reader can choose on of the posts to display in more detail for reading.

## Blog Post List View

#### First Step:
As with any new view we want to create, we start with the view function:

```python
from django.shortcuts import render
from .models import Post


def list_posts(request):
  posts = Post.objects.all() #1
  context = {
    'post_list': posts, #2
  }
  return render(request, "post_list.html", context)

```

The code is identical to a [regular view in Django]({{< ref "courses/350/blog-project/views.md" >}}), so we will describe only the new lines related to fetching the data:
- Line #1: This is the statement that instructs Django to fetch all posts from the database. It consists of the following parts:
  - `posts =`: This is the variable that will hold the data fetched from the database. Since the data could include multiple posts, it will be a list of post objects. Everything you know about python lists applies here, but because it also allows for additional commands, it will be known as a **QuerySet**.
  - `Post`: This is the Post model. It means the command we are issuing to Django applies to the Post objects only.
  - `objects`: This is known as the model manager. All the commands that we can perform on the database table that contains the Post information is found under this objects model manager. When you read the line `Post.objects`, it should mean to you that we are performing an operation on all the Post objects (or records) in the database.
  - `all()`: This is the fetch operations. We want to fetch all Post objects. Later we will see that there are other function such as filter, that allow us to filter specific objects from all the Post objects in the database.
- Line #2: Now that all the Post objects are stored in a list variable named `posts`, we want to deliver this data to the template so the template can display it. As we did with previously when [using templates for regular regular Django views]({{< ref "courses/350/blog-project/views.md" >}})


#### Second Step:

After creating the view, the next step is to wire the view to a url path. Since we previously [created a urls.py specific for our blog app]({{< ref "courses/350/blog-project/urls.md#improved-url-organization" >}}), we just need to update the `blog/urls.py` file to associate our `list_post` view with a path: 


```python
from . import views 
from django.urls import path

urlpatterns = [
    path('', views.list_posts), #1
]
```
Code explanation:
- Line #1: We placed all the paths for our blog url under the main path `/blog` when we improved [our app urls]({{< ref "courses/350/blog-project/urls.md#improved-url-organization" >}}). Therefore, associating a view function in `blog/urls.py` with an empty path means that it will be associated with the main `/blog` path only without any part after it. So to get the list, we access the path `/blog`.

#### Third Step:

Now all that remains is to create the template file `post_list.html` that we refered to [in `list_posts` view]({{< ref "#first-step" >}}). We must place the file in `/blog/templates/` and create the directory `templates` if it does not exist. 

**IMPORTANT NOTE:** Django is case sensitive. The templates directory must be named `templates` and placed inside `blog` directory.

This is how `blog/templates/post_list.html` will look like:

```html
<!doctype html>
<html lang="en">
  <head><title>Post List</title></head>
  <body>
    <h1>Latest posts:</h1>
    <ul>
      {% for post in post_list %}
      <li>{{ post.title }}, posted on {{ post.created_on }}</li>
      {% endfor %}
    </ul>
  </body>
</html>
```

We placed our list of post objects in the slot `post_list` when we constructed the context dictionary in [in `list_posts` view]({{< ref "#first-step" >}}). Since the posts objects are in a list, we can use the template for loop to loop over them and display them as an unordered list. The result is:

{{< figure src="courses/350/django-ddv-result.png" >}}

---

## Database Queries

Remember this line from `views.list_posts`:

```python
posts = Post.objects.all()
```

This line is called a query. A query is an operation used to fetch data from a database. It is however a simple query and fetches all the posts in the database. What if we need a specific subset of the posts that match some criteria. For that we used filtered queries.


### Filtered Queries

To perform filtered queries we replace `all()` in our query with `filter()`. The filter function allows us to use the lookup query syntax to specify the conditions in which we select our Post objects. Here is a filtered query where we select all Post objects that have the status value 1 (which means they are published, see [the models.py file]({{< ref "courses/350/blog-project/models.md" >}}) for details)

```python
posts = Post.objects.filter(status=1)
```
In this query, `status` is the name of the field and `1` is the value we are interested in. This is a lookup query where we perform exact value matching and the lookup syntax is simple:
```
field=value
``` 
- **Notice** we use =, not ==, this is very important

To perform more complex queries, you will have to use the [lookup query functions](https://docs.djangoproject.com/en/3.2/ref/models/querysets/#field-lookups) and a slightly different syntax:

```
field_name__lookup_function = value
```

After the field name in your query, you use double underscore __ then add the special lookup function. The list of [lookup functions can be found in the Django documentation](https://docs.djangoproject.com/en/3.2/ref/models/querysets/#field-lookups).

The choice of the lookup function will depend on the type of data in the field you are querying and the matching operation you want to perform.

### Queries on String Based Fields

These include CharField, TextField, SlugField, URLField, and EmailField. The main lookup functions you can use are:

| lookup function | Description                                                                                  |
| --------------- | -------------------------------------------------------------------------------------------- |
| contains        | Looks for all objects in which the queried field contains the lookup value                   |
| icontains       | same as contains but case insensitive                                                        |
| exact           | Looks for all objects in which the queried field contains an exact match of the lookup value |
| iexact          | same as exact but is case insensitive                                                        |
| startswith      | Looks for all objects in which the queried field starts with the lookup value                |
| istartswith     | same as startswith but is case insensitive                                                   |
| endswith        | Looks for all objects in which the queried field ends with the lookup value                  |
| iendswith       | same as endswith but is case insensitive                                                     |


#### Usage Examples

To fetch all posts with the word 'first' in the title using case insensitive search:

```python
Post.objects.filter(title__icontains='first')
```

To fetch all posts in which the body ends with the sentence `thank you.` using case insensitive search:

```python
Post.objects.filter(body__iendswith='thank you.')
```

## Queries on Numeric Fields

These include IntegerField, DecimalField, and FloatField. Typically we would use exact matching when we look for a specific value, for example:

```python
posts = Post.objects.filter(status=1)
```

status in the previous query is an IntegerField, and so we fetched all posts in which status is 1.

However, if we want to perform comparisons, we use the comparison lookup functions:

  - gt: Greater than
  - gte: Greater than or equals
  - lt: Less than
  - lte: Less than or equals

#### Example Usage

Imagine for example we have a web application with a Student model where we want to fetch all 3rd year and above students, we need to find students in which the value in `academic_year` (integer field) is greater than or equal to 3. The query would look like this:

```python
Student.objects.filter(academic_year__gte=3)
```


---

## Date/Time Lookups

- The typical date/time lookup methods can be classified into either:
  - Exact date/time lookup
  - Range lookup

---

## Exact Date/Time Lookups

- Using any combination of __year, __month, __day, __hour, __minute, and __second lookup to get a specific date
- For example...

---

### For posts created in the year 2020
```python
Post.objects.filter(create_on__year=2020)
```

---


### For posts in January 2020:
```python
Post.objects.filter(
  create_on__year=2020,
  create_on__month=1,
  )
```

---


### For posts in 23rd of January 2020:
```python
Post.objects.filter(
  create_on__year=2020,
  create_on__month=1,
  create_on__day=23,
  )
```

---

## Exact Date/Time Loockups

- How can you lookup posts created:
  - on the1st of every month?
  - at 2am (any date)
  - at 5pm on March 2nd (regardless of the year)
  - at 5pm on March 2nd in 2019 

---

## Range Lookup for Date/Time

- Ranged lookups can have 3 forms:
  1. Filter all dates BEFORE (Less than) a specific date/time 
  2. Filter all dates AFTER (Greater than) a specific date/time
  3. Filter all dates BETWEEN two dates/times

---

## Range Lookup for Date/Time

For all three cases you need to do the following:

1. Import datetime python library
2. The lookup dates/times must be either:
   - datetime.date object (for dates only)
   - datetime.datetime object (for date and time)
3. Use the date and datetime objects as the value to lookup
4. For datetime fields, use __date after field name to perform a date only lookup

---

## Filter Before a Date/Time Example

```python
import datetime
date_before = datetime.datetime(2019, 5, 3, 0, 0, 0)
posts = Post.objects.filter(created_on__lt=date_before)
```

- Can you tell the difference between using lt and lte here?
- What is the 0,0,0 part? (it's optional btw)
- What is the default time if we exclude it?

---

## Filter After a Date/Time Example

```python
import datetime
date_before = datetime.date(2019, 5, 3)
posts = Post.objects.filter(created_on__date__gt=date_before)
```

- Notice we are doing date comparison only here, see the __date after created_on
  - Django will ignore the time
- As with lt and lte, gt is exclusive, while gtw is inclusive of the query date.


---

## Check If Date/Time Has Passed


```python
import datetime
posts = Post.objects.filter(
  created_on__date__gt=datetime.datetime.now()
  )
```
- Use `datetime.datetime.now()`  or `datetime.date.today()`
- If date/time is 
  - gt now/today, then it's in the future
  - lt now/today, then it's in the past
  

---

## Between Dates/Times Lookup

- Same rules apply as with before and after lookup
- Use __range instead of __lt or __gt 
- Passed value must be a tuple containing the range dates/times
- The range is inclusive (like __lte and __gte)

---

## Between Dates/Times Lookup Example

```python
import datetime
start_date = datetime.datetime(2019, 1, 3)
end_date = datetime.datetime(2019, 3, 25) # after start_date
posts = Post.objects.filter(
  created_on__range=(start_date, end_date)
  )
```

- Range is from midnight start of start_date to midnight start of end_date, so Posts during end_date are not included
- Mixing of date with datetime in range is not allowed
- Range can be used with numeric fields also

---

## Filtering and Searching The List

- To add a search or filter feature to the list the following is needed
  1. A urlpatterns that accepts a query
  2. A view function that uses the query to filter the list
  3. Everything else remains the same

---


## Search/Filter Updated blog/urls.py

1. A urlpatterns that accepts a query:
   
```python
from . import views 
from django.urls import path

urlpatterns = [
    path('', views.list_posts),
    path('search/body/<str:q>/', views.search_posts),
]
```
  - Notice how the path has meaning
---

## Search/Filter Updated blog/views.py
2. A view function that uses the query to filter the list, Just add the following view function:
```python
def search_posts(request, q):
  posts = Post.objects.filter(body__icontains=q)
  context = {
    'post_list': posts,
  }
  return render(request, "post_list.html", context)
```

---

## Compare search_posts to list_posts

```python
def list_posts(request):
  posts = Post.objects.all()
  context = {
    'post_list': posts,
  }
  return render(request, "post_list.html", context)
```
---

## The Search View is Complete

- Included q argument for the query to search view function
- Used filter to get posts that match query
  - Here we searched the body
- Reused the same template post_list.html
- That's it!
- Can you do a search/filter for titles? or created_on dates?

---

## Complex Lookups

- If you want to use complex lookup conditions
- For example, a query that matches the body OR the title
- Read the documentation on [Django Complex Queries](https://docs.djangoproject.com/en/3.2/topics/db/queries/#complex-lookups-with-q-objects)

---

### Other interesting Lookups to Investigate

- in
- week, week_day, and quarter (for Date/DateTime)
- regex and iregex
- See [Djangos QuerySet Lookup documentation](https://docs.djangoproject.com/en/3.2/ref/models/querysets/#field-lookups)

---

### Fetching Single Objects

- Just replace filter with get
- get must return a single object (not a list) otherwise it will through an Exception
  - For our Post models, the exception classes are:
    - Post.DoesNotExist if object was not found
    - Post.MultipleObjectsReturned if multiple objects return (not unique)
- Typically use for primary key lookup

---

### Shortcut for Using Get

- Django provides the shortcut function `get_object_or_404` that doesn't through an error, but displays the 404 page instead
- 404 error means the page is not found
- Most common use case
```python
from django.shortcuts import get_object_or_404
from .models import Post

def my_view(request, pid):
  context = {
    post = get_object_or_404(Post, pk=pid)
  }
```

---

### Updating Blog to Show Post Details

Let's create the view for displaying a Post:

```python
def show_post(request, id):
  post = Post.objects.get(slug=id)
  context = {
    'post': post,
  }
  return render(request, "post_detail.html", context)
```

- We will get the id from the URL path, so we include it as a view function argument.
- Can you use get_object_or_404 instead?
---

### Updating blog/urls.py

List of urlpatterns should look like this:

```python
  urlpatterns = [
    path('', views.list_posts),
    path('search/body/<str:q>/', views.search_posts),
    path('<slug:id>/', views.show_post),
  ]
```

For show_post, Django take whatever slug is in the url and pass it as the id argument to the show_post view function

---

### Adding the Template

Add post_detail.html to blog/templates, it should contain the following:

```html
<!doctype html>

<html lang="en">
<head><title>{{ post.title }}</title></head>
  <body>
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
    <pre>Posted on: {{ post.created_on }}</pre>
    <pre>Updated on: {{ post.updated_on }}</pre>
  </body>
</html>
```

---

### The Result

{{< figure src="django-ddv-result2.png" >}}

Make sure you open the path /blog/blog-post-slug and replace blog-post-slug with the correct slug value for the post you want to view

---

### Adding Links from Post List View

Update the template post_list.html, specifically this line:

```html
  <li>{{ post.title }}, posted on {{ post.created_on }}</li>
```

Replace it with this:

```html
  <li>
    <a href="/blog/{{ post.slug }}">
      {{ post.title }}, posted on {{ post.created_on }}
    </a>
  </li>
```
Change it to make the title only clickable

---

### Result

{{< figure src="django-ddv-result3.png" >}}

Now you don't have to remember post slugs as they are now clickable







## Final Thoughts

- 
1. [Making queries documentation](https://docs.djangoproject.com/en/3.2/topics/db/queries/)(Required Reading!)
2. [QuerySet reference](https://docs.djangoproject.com/en/3.2/ref/models/querysets/)(See what is available to use)
  - Suggested methods to read about:
    - exclude, order_by, reverse, count, latest, earliest, first, last, exists
    - aggregate and annotate might seem confusing at this time, we will cover them later
  

## Review Questions and Challenges

- Create a view to fetch the list of unpublished posts
- What is the difference between the query lookup functions exact, iexact, contains, icontains?

