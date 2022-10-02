If you are working with Python, there is no escaping from the word “self”. It is used in method definitions and in variable initialization. The self method is explicitly used every time we define a method. In this article, we will get into the depth of self in Python in the following sequence:

What is the use of self in Python?
Python Class self Constructor
Is self in Python a Keyword?

What is the use of Self in Python?
Python - self in python - edureka
The self is used to represent the instance of the class. With this keyword, you can access the attributes and methods of the class in python. It binds the attributes with the given arguments. The reason why we use self is that Python does not use the ‘@’ syntax to refer to instance attributes. Join our Master Python programming course to know more. In Python, we have methods that make the instance to be passed automatically, but not received automatically.

Example:

```py
class food():
 
# init method or constructor
def __init__(self, fruit, color):
self.fruit = fruit
self.color = color
 
def show(self):
print("fruit is", self.fruit)
print("color is", self.color )
 
apple = food("apple", "red")
grapes = food("grapes", "green")
 
apple.show()
grapes.show()
```

Output:

> Fruit is apple
> color is red
> Fruit is grapes
> color is green



## **Python Class self Constructor**

self is also used to refer to a [variable](https://www.edureka.co/blog/variables-and-data-types-in-python/) field within the class. Let’s take an example and see how it works:

```py
class Person:
 
# name made in constructor
def __init__(self, John):
self.name = John
 
def get_person_name(self):
return self.name
```

## **Is self a Keyword?**

self is used in different places and often thought to be a keyword. But unlike in [C++](https://www.edureka.co/blog/object-oriented-programming-in-cpp/), self is not a keyword in Python.

self is a parameter in function and the user can use a different parameter name in place of it. Although it is advisable to use self because it increases the readability of code.

Example:

```py
class this_is_class:
def show(in_place_of_self):
print("It is not a keyword "
"and you can use a different keyword")
 
object = this_is_class()
object.show()
```

Output:

It is not a keyword and you can use a different keyword

With this, we have come to the end of our article. I hope you understood the use of self and how it works in Python.

*Check out the [Python Certification course](https://www.edureka.co/python-programming-certification-training)* *by Edureka. This* *Training course is designed for students and professionals who want to be a Python Programmer. The course is designed to give you a head start into [Python programming](https://www.edureka.co/blog/python-programming-language) and train you for both core and advanced concepts.*


