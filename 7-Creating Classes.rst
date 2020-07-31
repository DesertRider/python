Defining New Types
==================

Up to this point, we've been working with the built-in types that Python provides (str, int, float, etc.), but when we're modeling problems in our programs we often want to have more complex objects that fit our problem's domain. For instance, if we were writing a program to model information about cars (for an automotive shop) then it would make sense for us to have an object type that represents a car. This is where we start working will classes.

From this point on, most of the code that we'll be writing will be in files. Let's create a learning_python directory to hold these files that are really only there to facilitate learning.

::

    $ mkdir ~/learning_python
    $ cd ~/learning_python


Creating Our First Class

For this lesson, we'll use a file called creating_classes.py. Our goal is to model a car that has tires and an engine. To create a class we use the class keyword, followed by a name for the class, starting with a capital letter. Let's create our first class, the Car class:

~/learning_python/creating_classes.py:
::

    class Car:
        """
        Docstring describing the class
        """

        def __init__(self):
            """
            Docstring describing the method
            """
            pass

This is an incredibly simple class. A few things to note here are that by adding a triple-quoted string right under the definition of the class and also right under the definition of a method/function we can add documentation. This documentation is nice because we can even add examples in this string that can be run as tests to help ensure that our documentation stays up to date with the implementation.

A method is a function that is defined within the context of an object, and Python classes can define special functions that start with double underscores __, such as the __init__ method. This method overrides the initializer of the class. The initializer is what is used when we create a new version of our class by running code like this:

>>> my_car = Car()

We would like our Car class to hold onto a few pieces of data, the tires, and an engine. For the time being, we're just going to have those be a list of strings for the tires and a string for the engine. Let's modify our __init__ method to receive engine and tires as arguments:

~/learning_python/creating_classes.py
::

    class Car:
        """
        Car models a car w/ tires and an engine
        """

        def __init__(self, engine, tires):
            self.engine = engine
            self.tires = tires

What is self?

A big change from writing functions to writing methods is the presence of self. This variable references the individual instance of the class that we're working with. The Car class holds on to the information about cars in general in our program, where an instance of the Car class (self) could represent my Honda Civic specifically. Let's load our class into the REPL using python3.7 -i creating_classes.py, and then we'll be able to create a Honda Civic:

$ python3.7 -i creating_classes.py
::

    >>> civic = Car('4-cylinder', ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger'])
    >>> civic.tires
    ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger']
    >>> civic.engine
    '4-cylinder'

Once we have our instance, we're able to access our internal attributes by using a period (.).
Defining a Custom Method

The last thing that we'll do, to round out the first rendition of our first class, is to define a method that prints a description of the car to the screen:

~/learning_python/creating_classes.py
::

    class Car:
        """
        Car models a car w/ tires and an engine
        """

        def __init__(self, engine, tires):
            self.engine = engine
            self.tires = tires

        def description(self):
            print(f"A car with an {self.engine} engine, and {self.tires} tires")

Our description method doesn't have any actual arguments, but we pass the instance in as self. From there, we can access the instance's attributes by calling self.ATTRIBUTE_NAME.

Let's use this new method:
::

    $ python3.7 -i creating_classes.py
    >>> honda = Car('4-cylinder', ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger'])
    >>> honda.engine
    '4-cylinder'
    >>> honda.tires
    ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger']
    >>> honda.description
    <bound method Car.description of <__main__.Car object at 0x7fb5f3fbbda0>>
    >>> honda.description()
    A car with a 4-cylinder engine, and ['front-driver', 'front-passenger', 'rear-driver', 'rear-passenger'] tires

Just like a normal function, if we don't use parenthesis the method won't execute.
