# The Liskov Substitution Principle 


### 1. Definition

Subtypes must be substitutable for their base types.


### 2. When Is a Subtype Substitutable for Its SuperType?

A subtype doesn't automatically become substitutable for its supertype.**To substitutable, the subtype must behave like its supertype.**

An object's behavior is the contract that its clients can rely on. The behavior is specified by the public methods, any constraints placed on their inputs, any state changes that the object goes through, and the side effects from the execution of methods.

**Subtyping in Java requires the base class's properties and methods are available in the subclass.**

However, behavioral subtyping means that not only does a subtype provide all of the methods in the supertype, but it **must adhere to the behavioral specification of the supertype.** This ensures that any assumptions made by the clients about the supertype behavior are met by the subtype.



Relateds :
```
https://www.baeldung.com/java-liskov-substitution-principle
```

Tags :
```
#java #principle #liskov 
```
