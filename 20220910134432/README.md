# Effective Java Section 4 Item 17

## Minimize mutability
An immutable class is simply a class whose instances cannot be modified.The Java platform libraries contain many immutable classes, including String, the boxed primitive classes, and BigInteger and BigDecimal. There are many good reasons for this: Immutable classes are easier to design, implement, and use than mutable classes. They are less prone to error and are more secure.



To make a class immutable, follow these five rules:

- *Don’t provide methods that modify the object’s state*


