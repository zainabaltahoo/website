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

draft: True


---
{{% callout note %}}
Switch to branch **7-templates** from **malmarz/isom350-blog** github repo to see this step's implementation
{{% /callout %}}

This section assumed that you have an introductory understanding of HTML. Please read the following [introduction to HTML](https://www.w3schools.com/html/html_intro.asp) if you haven't worked with HTML before.

Templates are just strings. They are very similar to fstrings in Python, but must more sophisticated. If you remember with fstring, we can have string placeholders where python would plugin values from variables:

```python
my_name = "Mohammad"
greeting = f"Hello {my_name}"
print(greeting)
# Output: Hello Mohammad
```
Whatever the value contained in my_name, it will be placed by python in the slot `{my_name}`. Its a way to easily construct dynamic strings. Well templates are exactly just that. But instead of working simple short strings, templates are designed to be used with HTML files, which are just very long strings.

### Todo
- create template directory
- create html page with no placeholder
- create htmlpage with placeholder
