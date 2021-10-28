---
# Page title
title: Django Basics

# Title for the menu link if you wish to use a shorter link title, otherwise remove this option.
linktitle: Django Basics

# Date page published
date: 2021-03-23

# Academic page type (do not modify).
type: book

# Position of this page in the menu. Remove this option to sort alphabetically.
weight: 9

draft: False

# Featured image
# To use, place an image named `featured.jpg/png` in your page's folder.
# Placement options: 1 = Full column width, 2 = Out-set, 3 = Screen-width
# Focal point options: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight
# Set `preview_only` to `true` to just use the image for thumbnails.
image:
  placement: 1
  caption: "Python logo"
  focal_point: "smart"
  preview_only: false
  alt_text: Python logo

---
## What is Django?

Django is a web application development framework. Meaning, it is a set of rules, libraries, and conventions that you could use to streamline the process of building a web application.

Given that Django is a framework, it enforces a number of restrictions and ways to do things on our project. These restrictions would guarantee that we can gain the benefits promised by Django including improved collaboration, security, admin interface, reusability ...etc.

Django is classified as a fullstack framework that provides all the necessary libraries needed to build a web application from database abstraction to templating and everything in between. The alternative type of web frameworks are micro frameworks that specialize in a specific functionality of a web application. Flask is an example of a micro web framework that specializes in building view functions for handling HTTP requests. For templating or databases you have to use other libraries that can assist with these tasks such as Jinja for templating and SQLLAlchemy for databases.