# Effective Java Section 4 Item 18

## Favor composition over inheritance.

Inheritance is a powerful way to achieve code reuse, but it is not always the best tool for the job.Used inappropriately, it leads to fragile software.

**Unlike method invocation, inheritance violates encapsulation.** [example](https://github.com/Reza-Rahmani1378/effective-java/blob/develop/effective-java/src/main/java/com/amazon/effective_java/section4/item18/InstrumentedHashSet.java)

extending an existing class, give your new class a private field that references an instance of the existing class. This design is called composition because the existing class becomes a component of the new one. Each instance method in the new class invokes the corresponding method on the contained instance of the existing class and returns the results. This is known as forwarding, and the methods in the new class are known as forwarding methods. The resulting class will be rock solid, with no dependencies on the implementation details of the existing class. Even adding new methods to the existing class will have no impact on the new class. To make this concrete, here’s a replacement for InstrumentedHashSet that uses the composition-and-forwarding approach. Note that the implementation is broken into two pieces, the class itself and a reusable forwarding class, which contains all of the forwarding methods and nothing else. [example](https://github.com/Reza-Rahmani1378/effective-java/tree/develop/effective-java/src/main/java/com/amazon/effective_java/section4/item18/compostion).

**Inheritance is appropriate only in circumstances where the subclass really is a subtype of the superclass.** In other words, a class B should extend a class A only if an “is-a” relationship exists between the two classes. If you are tempted to have a class B extend a class A, ask yourself the question: Is every B really an A? If you cannot truthfully answer yes to this question, B should not extend A. If the answer is no, it is often the case that B should contain a private instance of A and expose a different API: A is not an essential part of B, merely a detail of its implementation. There are a number of obvious violations of this principle in the Java platform libraries. For example, a stack is not a vector, so Stack should not extend Vector. Similarly, a property list is not a hash table, so Properties should not extend Hashtable. In both cases, composition would have been preferable.


### Summary :
inheritance is powerful, but it is problematic because it violates encapsulation. It is appropriate only when a genuine subtype relationship exists between the subclass and the superclass. Even then, inheritance may lead to fragility if the subclass is in a different package from the superclass and the superclass is not designed for inheritance. To avoid this fragility, use composition and forwarding instead of inheritance, especially if an appropriate interface to implement a wrapper class exists. Not only are wrapper classes more robust than subclasses, they are also more powerful.



Tags :
```
#java #composition #inheritance
```

