# Java Effective Secction 1 item 3

## Enforce the singleton property with a private constructor or an enum type

A singleton is simply a class that is instantiated exactly once.

### Implementaion Singleton :

There are two common ways to implement singletons. Both are based on
keeping the constructor private and exporting a public static member to provide
access to the sole instance.

#### Singleton with pubilc static final field.


#### Singleton with static factory.






### Advantages :

 * The main advantage of the public field approach is that the API makes it clear that the class is a singleton: the public static field is final, so it will always contain the same object reference.

 * The second advantage is that it's simpler.

 * A final advantage of using a static factory is that a method reference can be used as a supplier.





### Note :

To maintain the singleton guarantee, declare all instance fields transient and provide a readResolve method (Item 89). Otherwise, each time a serialized instance is deserialized, a new instance will be created, leading, in the case of our example, to spurious Elvis sightings.To prevent this from happening, add this readResolve method to the Elvis class.




### Sumary :
a single-element enum type is often the best way to implement a singleton.

Relateds : 
```
 * <https://docs.oracle.com/javase/specs/jls/se11/html/jls-8.html#jls-8.9">
```
Tags :
```
 #java #singleton #enum #static_factory #public_final_field #effective-java #design_pattern #serialized  
```
