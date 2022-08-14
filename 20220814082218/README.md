# # Java Effective Section 1 item 1

Advantages And Disadvantages of Static Factory Method :

1-One advantage of static factory methods is that, unlike constructors, they
have names.

2-A second advantage of static factory methods is that, unlike constructors,
they are not required to create a new object each time they’re invoked.

3-A third advantage of static factory methods is that, unlike constructors,
they can return an object of any subtype of their return type.


4-A fourth advantage of static factories is that the class of the returned
object can vary from call to call as a function of the input parameters.

5-A fifth advantage of static factories is that the class of the returned object
need not exist when the class containing the method is written.



Disadvantages :

1-The main limitation of providing only static factory methods is that
classes without public or protected constructors cannot be subclassed.

2-A second shortcoming of static factory methods is that they are hard for
programmers to find.

Tags:
```
#java #static_method #factory #constructor
```

