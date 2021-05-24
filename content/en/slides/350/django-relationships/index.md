---
title: Traversing Relationships
summary: How we can traverse relationships in django objects and fetch/present them appropriately in views/templates
authors: []
tags: [isom350]
categories: []
date: "2021-05-24T05:06:22Z"
draft: true
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

Traversing Relationship

---

### Relationship in Django

- Represented in models using
  - ForeignKey
  - OneToOneField
  - ManyToMany Field

---

### Updating our Blog App

- Each blog post will have multiple comments
- Comment author will provide comment, optional name, and optional email
- Comments will be displayed along with author name in order below the post
- Date/Time of comment will be displayed next to it
- Number of comments and date/time of latest comment will be shown next to each post in post list

---

### Updated ERD

```mermaid
erDiagram
    POST ||--o{ COMMENT : Has

    POST {
        string title
        string slug
        string body
        datetime created_on
        datetime updated_on
        int status 
    }

    COMMENT{
        string comment
        string author
        string email
        datetime created_on
    }
    
```
---

### Updated Models.py

```python
class Comment(models.model):
  comment = models.TextField()
  author = models.CharField(max_length=100, blank=True, null=True)
  email = models.EmailField(blank=True, null=True)
  post = models.ForeignKey('Post', on_delete=models.CASCADE) 
```

---

### Admin and Migrations

- Create an inline Admin for the Post
- Don't forget makemigrations and migrate, why?
- Create at least 2 posts
- Create 2 comments for 1st post, and 3 comments for 2nd post.

---

### Traversing Relationship

- How do we display comments for each post?

---

{{< figure src="django-ddv-result2.png" >}}