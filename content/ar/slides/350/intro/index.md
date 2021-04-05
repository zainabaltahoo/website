---
title: Slides
summary: ISOM 350 Introduction
authors: []
tags: []
categories: []
date: "2019-02-05T00:00:00Z"
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
    theme: base

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
    history: true
---

# ISOM 350
## Business Application Development

Mohammad AlMarzouq

Spring 2021

---

## Course Website

[malmarz.netlify.app](https://malmarz.netlify.app)

---

## Syllabus

[bit.yl/mis350_syl](https://bit.yl/mis350_syl)

---

## Requirements

- Read the [Syllabus](https://bit.ly/mis350_syl)
- Signup for [class replit team](https://replit.com/teams/join/slpharshbwpedtcbfdfsnrkqjlkjpabh-miscba)
- Signup for [github.com](https://github.com/join)
- Completion of an introductory course in programming (Doesn't have to be Python)
- Get familiar with [Django's Documentation](https://docs.djangoproject.com/en/3.1/)

---

All instructions available on course website.

---

## Grade Distribution

| Item | Grade |
|---|---|
|  Quizzes | 20%  |
|  Assignments | 20%  |
|  Lab | 10%  |
|  Final Project | 30%  |
|  Final Written | 20% |
|---|---|
| Total | 100% |


---

## Exercises and Assignments

- Building blog platform in class
- Polling application for assignments
  - Bi-weekly Assignments
  - Requirements detailed on website
- Bi-weekly written Quizzes
- Team based final project
  - Start forming teams of 3
  - Prepare a paragraph describing your project


---

## The Introduction

1. [Quick Python review, including Object Oriented]({{< ref "courses/350/intro/python.md" >}}) Programming and some useful Python features.
2. [Remote collaboration]({{< ref "collab.md" >}}) on software projects.
3. [Project management]({{< ref "proj-mgt.md" >}}) for team based projects.
4. [Overview of web applications]({{< ref "webapplications.md" >}}).
5. [Overview of the Django development process]({{< ref "dev-process.md" >}}).

---

## The Python Review

- Will be covered in the lab
- Will touch upon some advanced topics in class
  - Exceptions
  - List comprehensions
  - Object Oriented Programming

---

## The Python Syntax

You can easily transfer what you learned in VB to Python, for example:

```
If x > 5 Then
    ` Do something like display this message
    MsgBox("the condition is True!")
End If
```
What does the code do?


---


## The Python Syntax

In Python you would write it as:
```python
if c > 5:
    # Do something like display this message
    print("The condition is True!")
```


---

## From VB to Python

Almost everything you learned in VB is transferrable to Python, including:

- Functions and subroutines
- If statements
- Loops
- Variables ... etc

Will be covered in more detail in the lab, but you can get a head start by [reading the resources in class website]({{< ref "courses/350/intro/python.md#online-resources" >}})


---

## Exceptions

- Executes code when a certain condition is met!
- **Exactly** like if statements
  - But different in how it does it.

---

## Exceptions

- If statements evaluate the condition before executing the conditional code
- With exceptions, we tell Python that we expect an error (also known as exception) to occur in some part of our code. 
  - Only when the expected error occurs does python execute the conditional code
  
---

## Exceptions Example

```python
try: 
    received_data = socket.read() 
except IOException as ioe: 
    print("Connection disconnected") 
```

---

## List Comprehensions

- Shortcut for constructing a list from another list.
- For example, if we had the follow list:


```python
data = [2, 3, 4, 5, 10, 34, 1]
```

---

## List Comprehensions

- We can create a new list containing even numbers only using:

```python
even_numbers = []
for x in data:
    if x % 2 == 0:
        even_numbers.append(x)
```

---

## List Comprehensions

- Using list comprehensions it's just a single line!:

```python
even_numbers = [x for x in data if x % 2 == 0]
```
- The syntax is:

```python
[ `expression on elem` for elem 
  in list_var 
  `optional if statement`]
```

---

## Object Oriented Programming (OOP)

- Using functions improves the organization of a program
- Reflects the experience of the developer
- Improves the readability and ability to collaborate
- It is considered an improvement over simply writing structured statements in a single file

---

## Object Oriented Programming (OOP)

- OOP is a code organizational improvement over using functions.
- With functions you might have a student registration program that looks like this:

```python
student_recods = []
courses = []
def register_student_in_course(student, course): #...
def drop_student_in_course(student, course): #...
def list_students_in_course(course): #...
```

---

## Object Oriented Programming (OOP)

- Notice how when using functions, we create:
  - Variables to hold data
  - Functions to perform tasks
- Variables and functions are independent

---

## Object Oriented Programming (OOP)

- In OOP we combine related data and functions into a single unit called a class
- We organize course related information and functions into a single class which we call Course
- We organize student related information and functions into a single class which we call student
- This is how they might look like

---

```python
Class Student:
  def __init__(self, sname, sid):
    self.name = sname
    self.id = sid
  
  def register_course(self, course): # ...
  def drop_course(self, course): # ...

```

---

```python
Class Course:
  def __init__(self, cname):
    self.students = []
    self.name = cname
  
  def list_students(self): # ...

```

---

## Object Oriented Programming (OOP)

- Where is the benefit here?
  - Mainly in code reusability
  - OOP allows for **inheritance**
    - Meaning, that we can derive a new class from another

---

## Inheritance

- For example, we can create a new kind of student called, GraduateStudent.
- GraduateStudent behaves in the same way as the student class, but is able to teach some courses.
- So we **extend** the Student class to create a new GraduateStudent class as such:
  
```python
class GraduateStudent(Student):
  def teach_class(self, course): # ...
```

---

## Inheritance

- Now the GraduateStudent has all the variables and functions that are part of the Student class.
- We also added a teach_class function that is unique to the GraduateStudent
- We dont have to redefine the register_course or drop_course functions, we can just use them!
- With improved reusability, ability for a development team to coordinate improves

---

## Objects Vs Classes

- You cannot use classes like you do variable or function, you must create an instance of them
  - The operation is known as instantiation
  - It creates a new copy of the variables in the class
  - The new instance is known as an **object**
  - We use the functions and variables in the object NOT the class

```python
# THIS IS WRONG!

Student.register(course) # Which student will python register?

```

---

## Creating an Instance

```python
# Create a Student Instance where the name variable will be set
# to mohammed, and the id variable set to 1234
student = Student("mohammed",1234)

# Now we can use the functions
student.register_course(course)

print(student.name) # will print mohammed
```

---

## Objects Vs Classes

- Think of a class as a house blueprint (a plan)
- It tells us how the house will look like
- But we cannot live in it
- We can create many houses from it
- Each built house will have a different faimily living in it
- The built houses are all instances of the house designed in the plan

---

## Objects Vs Classes

- Similarly, we are all Human
- Human is the class
- Myself, an each one of you, is an instance of class Human
- We all have heads, hands, feet, and characteristics associated with humans
- Yet each of us is unique in that we have our own names and personal characteristics
- The individuals are the objects of class Human

---

## Objects Vs Classes

- Can you think of other examples?
- Can you think of variables and functions associated with these classes?

---

## Speaking of Functions and Variables

- In OOP, we no longer call functions defined in classes as functions
  - They are now called methods
  - But they are identical in every way to functions
  - Except it can work on the variables in the object

---

## Speaking of Functions and Variables

- Variables defined in objects also get a name change to distinguish them from regular variables
  - We call them instance variables or properties
  - Similarly, everything you know about variables apply to them
  - Only difference is scope
- The whole idea of putting variables in classes is to make them in scope for class methods for easy access

---

## Is OOP Really Useful?

- Anything you can build with OOP you can build with regular structured programming
- We did mention that OOP makes code more reusable and improves team collaboration
  - We will use Inheritence heavily with Django to reconfigure parts of Django for our needs
  - Without OOP the configurations that we need to do would become much more complex

---

## Is OOP Really Useful?

- Another improvement brought by OOP is how we think about System Analysis and Design
  - Now we try to group related functionality and data together
  - We think about code organization at analysis and design stage
  - Contemporary tools for visualizing SAD information builds heavily on OOP (e.g., UML)
- Even if you do not turn out to be a programmer understanding OOP will be critical for MIS majors.