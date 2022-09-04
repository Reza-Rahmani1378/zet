# Java Effective Section 3 Item 10 Part 1

## The easiest way to avoid problems is not to override the equals method:

- **Each instance of the class is inherently unique.**

- **There is no need for the class to provide a “logical equality” test.**

- **A superclass has already overridden equals, and the superclass behavior is appropriate for this class.**

- **The class is private or package-private, and you are certain that its equals method will never be invoked.**


## So when is it appropriate to override equals?

It is when a class has a notion of logical equality that differs from mere object identity and a superclass has not already overridden equals. This is generally the case for value classes. A value class is simply a class that represents a value, such as Integer or String. A programmer who compares references to value objects using the equals method expects to find out whether they are logically equivalent, not whether they refer to the same object. Not only is overriding the equals method necessary to satisfy programmer expectations, it enables instances to serve as map keys or set elements with predictable, desirable behavior.One kind of value class that does not require the equals method to be overridden is a class that uses instance control (Item 1) to ensure that at most one object exists with each value. Enum types (Item 34) fall into this category. For these classes, logical equality is the same as object identity, so Object’s equals method functions as a logical equals method.


## The equals method implements an equivalence relation. It has these properties:

- Reflexive: For any non-null reference value x, x.equals(x) must return true.

- Symmetric: For any non-null reference values x and y, x.equals(y) must return true if and only if y.equals(x) returns true.

- Transitive: For any non-null reference values x, y, z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) must return true.

- Consistent: For any non-null reference values x and y, multiple invocations of x.equals(y) must consistently return true or consistently return false, provided no information used in equals comparisons is modified.


- For any non-null reference value x, x.equals(null) must return false.






