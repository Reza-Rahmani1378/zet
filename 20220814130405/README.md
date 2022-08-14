# Java Effective Section 1 item 2 

## Consider a builder when faced with many constructor parameters



Disadvantage Of Constructor for many paramters : 

In short, the telescoping constructor pattern works, but it is hard to write
client code when there are many parameters, and harder still to read it.

we can use the JavaBeans pattern instead of constructor and this design pattern has advantages and disadvantages :


Addvantages :

 * This pattern has none of the disadvantages of the telescoping constructor pattern.


Disaddvantages :
 
 * a JavaBean may be in an inconsistent state partway through its construction.
 * A related disadvantage is that the JavaBeans pattern precludes the possibility of making a class immutable.




Luckily, there is a third alternative that combines the safety of the telescoping
constructor pattern with the readability of the JavaBeans pattern. It is a form of the
Builder pattern.

### Design Pattern Builder :
 
 * Instead of making the desired object directly, the client calls a constructor (or static factory) with all of the required parameters and gets a builder object. Then the client calls setter-like methods on the builder object to set each optional parameter of interest.

 * The Builder pattern is well suited to class hierarchies.


#### Advantages :

 * A minor advantage of builders over constructors is that builders can have mul-tiple varargs parameters because each parameter is specified in its own method.

 * Alternatively, builders can aggregate the parameters passed into multiple calls to a method into a single field, as demonstrated in the addTopping method earlier.
 
 * The Builder pattern is quite flexible. A single builder can be used repeatedly to build multiple objects.


#### Disadvantages :
 
 * The Builder pattern has disadvantages as well. In order to create an object, you must first create its builder. While the cost of creating this builder is unlikely to be noticeable in practice, it could be a problem in performance-critical situations.


#### Summary :

In summary, the Builder pattern is a good choice when designing classes
whose constructors or static factories would have more than a handful of
parameters, especially if many of the parameters are optional or of identical type.


Ralted : 
```
*
<https://github.com/Reza-Rahmani1378/effective-java/tree/develop/effective-java/src/main/java/com/amazon/effective_java/section1/item2/builder_design_pattern/book>

```


Tags :
```
#java #builder #constructor

```
