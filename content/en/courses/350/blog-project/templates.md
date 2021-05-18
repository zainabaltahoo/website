---
# Page title
title: Templates

# Title for the menu link if you wish to use a shorter link title, otherwise remove this option.
linktitle: Templates


# Date page published
date: 2021-03-23

# Academic page type (do not modify).
type: book

# Position of this page in the menu. Remove this option to sort alphabetically.
weight: 7

draft: true


---
{{% callout note %}}
Switch to branch **7-templates** from **malmarz/isom350-blog** github repo to see this step's implementation
{{% /callout %}}

This section assumed that you have an introductory understanding of HTML. Please read the following [introduction to HTML](https://www.w3schools.com/html/html_intro.asp) if you haven't worked with HTML before.

Templates are just strings. They are very similar to fstrings in Python, but much more sophisticated. If you remember with fstring, we can have string placeholders where python would plugin values from variables:

```python
my_name = "Mohammad"
greeting = f"Hello {my_name}"
print(greeting)
# Output: Hello Mohammad
```
Whatever the value contained in my_name, it will be placed by python in the slot `{my_name}`. Its a way to easily construct dynamic strings. Well templates are exactly just that. But instead of working simple short strings, templates are designed to be used with HTML files, which are just very long strings.

We used fstrings in the [previous section on views]({{< ref "/courses/350/blog-project/views" >}}) to construct dynamic HTML. However, it was not very elegant to have HTML and python code in the same file. Furthermore, it would be very inconvenient for designers to work on fstrings. This is where Django templates are truly useful. Templates separate HTML text into their own `.html` file away from python code. In the view function, we just instruct Django which template file to use. Because template files are `.html` files, designers can use the tools they are accustomed to, to design the page. Developers can build minimal templates to get the web app working, then replace them with the well designed files provided by the designers.

- using templates
- taking advantage of template variables, tags, and filters

### Todo
- create template directory
- create html page with no placeholder
- create htmlpage with placeholder
