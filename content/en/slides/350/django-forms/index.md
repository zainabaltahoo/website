---
title: Django Forms
summary: How to use Django forms to handle data input
authors: []
tags: [isom350]
categories: []
date: "2021-06-06T12:33:41Z"
draft: false
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

Django Forms

---

### What Are Forms?

- HTML component 
- Used to send user input to server
- POST forms include data in the body
- GET forms include data in the url
- Submit button is needed to perform send action
  ```html
  <form>
    <!-- data input components here -->
    <input type=submit>
  </form>
  ```

---

### What is the Role of Django Forms

- Manages the creation of the data input components
  - Template must still include the form and submit tags
  - Can Auto generate forms based on models definition
- Manages security of forms
  - Data submission in web apps is very risky
  - Tries to prevent exploits and modification

---

### Using Django Forms

- Define forms in forms.py
  - Very similar to models
- Use forms in views that accept user input
  - Standard steps to using forms


---

### Updating Blog App to Use forms

- We would like to create a view that enables writing a blog post and avoid using the Django admin
- This view is a data creation view (from CRUD)
  - It allows for the creation of posts
  - So we define a form that allows the user to enter data needed for a post

---

### The Post Model

```python
class Post(models.Model):
  title = models.CharField(max_length=200, unique=True)
  slug = models.SlugField(max_length=200, unique=True)
  body = models.TextField()
  created_on = models.DateTimeField(auto_now_add=True)
  updated_on = models.DateTimeField(auto_now=True)
  status = models.IntegerField(choices=STATUS, default=0)
```

- User will post the title and body.
- Slug is auto-generated from title
- Status is unpublished by default
- Dates are auto-inserted

---

### The Post Form

- Create blog/forms.py:
```python
from django import forms

from .models import Post

class PostForm(forms.ModelForm):
  class Meta:
    model = Post
    fields = ["title", "body"]
```
---

### The PostForm

- Notice how PostForm inherits from forms.ModelForm
- A model form is a Django form based on a Django model
  - We set the model as Post
  - Django will choose best input components based on the model field types
- in the fields attribute, we are telling Django what input the user will provide
  - In this case it is title and body

---

First Without Auto-Creating The Slug Field Value

---

### The create_post View 

```python
from django.shortcuts import render, redirect

from .forms import PostForm

def create_post(request):
  form = PostForm(request.POST or None)

  data = {}
  data["form"] = form

  if form.is_valid():
    post = form.save()
    return redirect("show-post", s=post.slug)

  return render(request, 'create_post.html', data)
```

---

```python
from django.shortcuts import render, redirect

```

- Notice we have imported the redirect function
- Used like render
- Forces the browser to open a specific page
  - We will need to give urls paths names for easy referral

---
```python
from .forms import PostForm
```

- We must import the PostForm we created in forms.py

---
```python
  form = PostForm(request.POST or None)
```

- Here we are creating the form
- Notice the argument is request.POST or None
  - It means if there is data coming from the client, give it (bind it) to the form
    - The form will allow us to validate the data
  - Otherwise, create an empty form

---

```python
  data = {}
  data["form"] = form
```

- We are putting the form in the context to deliver it to the template
- It will be displayed in the template

---

```python
  if form.is_valid():
    post = form.save()
    return redirect("show-post", s=post.slug)
  return render(request, 'create_post.html', data)
```

- The if statement will only be true if Django receives valid data from the client
- form.save() used to create a new post from the submitted data
- Redirect will send the client to the show-post view
- The create_post.html template is only shown is data is not valid or empty

---

```python
  return redirect("show-post", s=post.slug)
```
- For redirect to work we must give our paths in urls.py names:
```python
  path('post/<slug:s>/',views.show_post, name="show-post"),
```
- We gave the show_post path the name `show-post`
- Can be any name but must be unique for redirect to find the path
- The second argument in redirect `s=` must match the name of the slug pattern s in the path 


---


### Updated urls.py

- Add the following entry to wire the view in urls.py:

```python
  path('create/post/',views.create_post)
```

---

### The create_post.html Template

```html
<form action="." method="POST">
  {% csrf_token %}
  {{ form.as_p }}
<input type="submit" value="Submit">
</form>
```
- We must include the form (with action and method) and submit button
- csrf_token tag must be there for Django to manage security
- {{ form.as_p }} displays each component of the form inside a p tag
  - Try also {{ form.as_table }}

---

- The create_post view is complete
- Problem is we did not provide a slug for the posts
- This will create problems, so we must modify our code

---


Now With Auto-Creating The Slug Field Value

---

### The create_post View 

```python
from django.utils.text import slugify

from .forms import PostForm

def create_post(request):
  form = PostForm(request.POST or None)

  data = {}
  data["form"] = form

  if form.is_valid():
    post = form.save(commit=False)
    post.slug = slugify(post.title)
    post.save()
    return redirect("show-post", s=post.slug)

  return render(request, 'create_post.html', data)
```

---

### The Update

- Everything remained the same except this part:

```python
  post = form.save(commit=False)
  post.slug = slugify(post.title)
  post.save()
```

---

```python
  post = form.save(commit=False)
```
- Here a post object was created but was NOT stored in the database
- This allows us to modify the data in the object

---

```python
  post.slug = slugify(post.title)
  post.save()
```

- Here we modify the slug field by slugifying the title
- We imported the slugify function that converts any string into a slug
- Then we save the post in the database

---

### The Result


{{< figure src="django-forms-result.png" width="35%" height="35%" >}}

Here is the create post view with the form

---

### The Result


{{< figure src="django-forms-result2.png" width="35%" height="35%" >}}

Forms will ensure input data is valid and give appropriate errors automatically

---

- Upon successful submission of data, the browser will be redirected to the newly created post
- Because we used redirect instead of render
- Can you modify the view to redirect to the post list instead?

---

### Using Form in Existing Views

- Forms can also be used in existing views
- Let's add a comment form to the show_post view
- Which allows readers to write comments

---

### Creating The Form

- Update blog/forms.py:

```python
from .models import Post, Comment

class CommentForm(forms.ModelForm):
  class Meta:
    model = Comment
    fields = ["comment", "author", "email", "post"]
    widgets = {
      'post': forms.HiddenInput(),
    }
```
- Explain what's going on
- widgets allows us to change how a field will be displayed in a form
  - Remove it and see what happens

---

### Updating show_post View

```python
def show_post(request, s):
  obj = Post.objects.get(slug=s)
  comments = obj.comment_set.all()
  data = {}
  data["post"] = obj
  data["comment_list"] = comments
  
  form = CommentForm(request.POST or None, initial={"post":obj.pk} )
  data["comment_form"] = form
  if form.is_valid():
    form.save()
    return redirect("show-post", s=obj.slug)
  
  return render(request, "post_detail.html", context=data)

```

---

### The Changes

- Everything remained the same except this part:

```python
  form = CommentForm(request.POST or None, initial={
    "post":obj.pk
  }) 
  data["comment_form"] = form
  if form.is_valid():
    form.save()
    return redirect("show-post", s=obj.slug)
```

- You should be able to explain what is happening here

---

### Setting The ForeignKey

- Because a comment must be related to a post, we give the form the primary key value of the post using initial argument:

```python
form = CommentForm(request.POST or None, initial={
  "post":obj.pk
  })
```

---

### The Initial Argument

- Accepts a dictionary
- Will match keys to field names in the form
- Will use matching value to populate the fields with an initial value
- Used to set ForeignKeys or the value of any other field
- Can set the values of multiple fields as a time
  - Just include more key-value pairs in the dictionary

---

### Widgets

- Widgets are the UI components used to display on the browser
- Django will automatically select the appropriate widget for each model field
- We can use widgets field when defining the form to manually choose the widget
- List of available widgets can be found in the [Django Form Field Widgets documentation](https://docs.djangoproject.com/en/3.2/ref/forms/widgets/)