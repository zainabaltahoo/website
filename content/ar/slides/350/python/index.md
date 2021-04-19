---
title: Python Review
summary: Review of main Python concepts needed in this course along with the introduction of some advance concepts like exceptions, list comprehensions, and OOP
authors: []
tags: [isom350]
categories: []
date: "2021-04-14T13:12:45Z"
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

Python Review

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
if x > 5:
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
  # Executes if connection disconnects
  print("Connection disconnected") 
```

### Compared to if:

```python
if x > 5:
  # Executes if condition is True
  print("The condition is True!")
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

---

## The syntax 

```python
list_var = [ `left part` `middle part` `right part`] 
```
- **list_var:** Variable containing new list
- **[ brackets ]**: Brackets are required because we are creating a list
- **middle part:** is the for loop syntax
- **left part:** the operation you want to perform on the loop var
- **right part:** is the *optional* condition

---

### List Comprehension Examples

With condition and loop var x ont changed:
```python
even_numbers = [x for x in data if x % 2 == 0]
```

Without condition and loop var x is squared:
```python
squared_numbers = [x**2 for x in data]
```
Or use functions/methods that return values on loop var x:
```python
upper_case_names = [x.upper() for x in data]
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

## Simple Class Example

```python
class Student:
  pass

# to use it we must create instance
s1 = Student()
s1.name = "Mohammad"

s2 = Student()
s2.name = "Ahmed"
```

There is no uniform structure for variable... let's fix this


---

## Using Constructors

Constructor would allow us to set instance variables at time of instantiation:
```python
class Student:
  def __init__(self, sname, sid):
    self.name = sname
    self.id = sid

# Creating instances
s1 = Student("Mohammad", 123)
s2 = Student("Ahmed", 124)
```
Now all instances will have a name and sid, but what about functions?

---

## Adding Functions (Methods)

Just define the methods as part of the class.
```python
class Student:
  def __init__(self, sname, sid):
    self.name = sname
    self.id = sid
  
  def register_course(self, course): # ...
  def drop_course(self, course): # ...

# using methods:
s1 = Student("Mohammad", 123)
s1.register_course(c)
```

Methods are used on instances but defined in classes.

---

# Improved Example

We can also create a class for Courses:
```python
class Course:
  def __init__(self, cname):
    self.students = []
    self.name = cname
  
  def list_students(self): # ...

```
Can you think of other classes that fit this example?

---

## Objects Vs Classes

- You cannot use classes like you do variable or function, you must create an instance of them
  - The operation is known as instantiation
  - It creates a new copy of the variables in the class
  - The new instance is known as an **object**
  - We use the functions and variables in the object NOT the class

```python
# THIS IS WRONG!

Student.register_course(course) # Which student will python register?

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
  - We call them instance variables, properties, or attributes
  - Similarly, everything you know about variables apply to them
  - Only difference is scope
- The whole idea of putting variables in classes is to make them in scope for class methods for easy access

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

- The Class GraduateStudent is now a SubClass of Student Class.
- The Student class is now a SuperClass of the GraduateStudent class.

---

## Inheritance

- Now the GraduateStudent has all the variables and functions that are part of the Student class.
- We also added a teach_class function that is unique to the GraduateStudent
- We don't have to redefine the register_course or drop_course functions, we can just use them!
- With improved reusability, ability for a development team to coordinate improves

---

## Creating an Instance

```python
# Create a Student Instance where the name variable will be set
# to mohammed, and the id variable set to 1234
s1 = Student("mohammed",1234)

# Now we can use the functions
s1.register_course(course)

print(s1.name) # will print mohammed
```

---


## Creating an Instance of a SubClass

```python
# The GraduateStudent subclass uses the same constructor
s2 = GraduateStudent("Abdullah",2345)

# But has the additional method we defined
s2.teach_course(course)

# Methods from Student class can also be used
s2.teach_course(grad_course)

# Properties from Student class also exist
print(s2.name) # will print abdullah

```

---

## Extending Methods in SubClasses

- If we want to change the implementation of methods in subclasses, just redefine them, this includes **the constructor**:

```python
class GraduateStudent(Student):
  def __init__(self, name, sid):
    # redefine the constructor to do something different here
    self.thesis_title = #....
    self.name = name
    self.sid = sid
    
  def teach_class(self, course): # ...
```

GraduateStudent will use the newly defined constructor

---

## Using super

- When redefining methods, you can even reuse the method from the SuperClass:
```python
class GraduateStudent(Student):
  def __init__(self, name, sid):
    # This will execute the same method from the super class
    super().__init__(name, sid)
    # Then you can do additional stuff 
    # specific for GraduateStudents
    self.thesis_title = #....


  def teach_class(self, course): # ...
```
GraduateStudent will use the newly defined constructor but execute the Student constructor first.

---

## Is OOP Really Useful?

- Anything you can build with OOP you can build with regular structured programming
- We did mention that OOP makes code more reusable and improves team collaboration
  - We will use Inheritance heavily with Django to reconfigure parts of Django for our needs
  - Without OOP the configurations that we need to do would become much more complex

---

## Is OOP Really Useful?

- Another improvement brought by OOP is how we think about System Analysis and Design
  - Now we try to group related functionality and data together
  - We think about code organization at analysis and design stage
  - Contemporary tools for visualizing SAD information builds heavily on OOP (e.g., UML)

---

### Even if you do not turn out to be a programmer understanding OOP will be critical for MIS majors.

---

## Other Useful Tip

- You can change what message is displayed if an object of a class was printed by redefining the special `__str__` method.
- For example:
  
```python
s1 = Student("mohammed",1234)
print(s1) 
# will display:
# <__main__.Student object at 0x7fb768be4910>
```

---

## Redefining The __str__ Method

- Let's add the `__str__` method that just returns a string.
- We can use fstrings and reference instance variables using `self.`
- Notice here we want to include the name and if stored in the object:
  
```python
class Student:
  #..
  def __str__(self):
    return f"<Student {self.name} {self.id}>"
  #..
```

---

## The Output

- Now printing the Student object will give a different output:

```python
s1 = Student("mohammed",1234)
print(s1) 
# will display:
# <Student mohammed 1234>
```


---


## Video Summary of OOP

Be sure to view the whole 6 video series

{{< youtube ZDa-Z5JzLYM >}}