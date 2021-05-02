---
title: Django View Functions
summary: Explains how Django view functions work and how to use them
authors: []
tags: [isom350]
categories: []
date: "2021-05-02T20:46:46Z"
slides:
  # Choose a theme from https://github.com/hakimel/reveal.js#theming
  theme: moon
  # Choose a code highlighting style (if highlighting enabled in `params.toml`)
  #   Light style: github. Dark style: dracula (default).
  #   Available highlight themes listed in: https://highlightjs.org/static/demo/
  #   Use lower case names and replace space with hyphen '-'
  highlight_style: dracula

  diagram: true
  diagram_options:
    # Mermaid diagram themes include: default,base,dark,neutral,forest
    theme: dark

  # RevealJS slide options.
  # Options are named using the snake case equivalent of those in the RevealJS docs.
  reveal_options:
    controls: true
    progress: true
    slide_number: c/t  # true | false | h.v | h/v | c | c/t
    center: true
    rtl: false
    mouse_wheel: true
    transition: concave  # none/fade/slide/convex/concave/zoom
    transitionSpeed: default  # default/fast/slow
    background_transition: slide  # none/fade/slide/convex/concave/zoom
    touch: true
    loop: false
    menu_enabled: true
    chalkboard_enabled: true
    history: true
---


# ISOM 350
## Business Application Development

Mohammad AlMarzouq

Django View Functions

---

## Django MVT Webapp Model

When constructing webapps, we build:

1. **Models:** To handle data
2. **Views:** To handle business logic
3. **Templates:** To handle how screens will look

We continue to work on models, views, and templates as we build a webapp

---

## View Functions

- Receive HTTP requests
- Perform a task
- Then return an HTTP response

---

## Understanding The View Function

In your app views.py:

```python
def test_view(request):
  print(f"Request: {request}")
```

---

## Continue With test_view

Now link the view function to a url path:

Update mysite/urls.py:

```python
from django.contrib import admin
from django.urls import path
from blog.views import test_view

urlpatterns = [
    path('admin/', admin.site.urls), 
    path('test/', test_view),    
]
```

---

## Test The New View

- Run the Django development server and you will notice:

{{< figure src="django-404.png" >}}

---

## What is Django Telling you?

1. 404 is a standard HTTP response code, it means that page you requested does not exist
   - Which page is that?
2. The available paths are `/admin/` and `/test/`
   - Where were they defined?
   - how can we fix the 404? do we need to?
   - How do we run our test_view?
---

## Continue Test The New View

- Point your browser to the path /test
- You need to pay attention to the output in two places:
  1. The browser
  2. The console (on replit.com)

---

{{< figure src="django-view-error.png" caption="What is this browser output telling us?" >}}

---

{{< figure src="django-console-error.png" caption="What is this console output telling us?" >}}

---

## Continue Test The New View

- Can you explain what just happened?
- How can we fix the ValueError?

---

## Solution

If your response was:
  
  Let `test_view` return an HTTP Response

Then you are correct!

---

## Fixing test_view

```python
from django.http import HttpResponse

def test_view(request):
  return HttpResponse("Hello World!")
```

---

## But What About HTML?

- Browsers are capable of rendering HTML
- Include HTML in the HttpResponse

```python
from django.http import HttpResponse

def test_view(request):
  return HttpResponse("""<html><body>
  <h1>Hello World!</h1>
  <p>This is my first <strong>html</strong> web app!</p>
  </body></html>""")
```

---

### Of course, we will not be writing HTML using Python Strings.

This is where Django Templates are most useful

---

## Django simplification of CRUD Views

- Most functions ina data-driven web app as CRUD operations
- We can reuse some ready made generic Django views for CRUD operations
  - We just have to configure them
- Alternatively, we can write the whole view function
  
---

## The Read Operation

Such operations are used to retrieve data from the database, then display it as:
1. A list
2. A single object

---

## For Single Objects

1. Subclass `DetailView` from `django.views.generic`
2. Define the `model` to use 
3. Define the `template_name`

---

## For Single Objects


```python
from django.views import generic
from .models import Post


class PostDetailView(generic.DetailView):
  model = Post
  template_name = 'post_detail.html'
```


---

## For List Views

1. Subclass `ListView` from `django.views.generic`
2. Define what list to show using `queryset` 
3. Define the `template_name`

---

## The List View

```python
from django.views import generic
from .models import Post


class PostListView(generic.ListView):
  queryset = Post.objects.filter(status=1).order_by('-created_on')
  template_name = 'post_list.html'
```

---

Can you tell what is missing to complete this web app?

---

## The Missing Parts

1. Creating a url path for each view
2. Providing the templates
