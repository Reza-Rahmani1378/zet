# The Liskov Substitution Principle 


### 1. Definition

Subtypes must be substitutable for their base types.


### 2. When Is a Subtype Substitutable for Its SuperType?

A subtype doesn't automatically become substitutable for its supertype.**To substitutable, the subtype must behave like its supertype.**

An object's behavior is the contract that its clients can rely on. The behavior is specified by the public methods, any constraints placed on their inputs, any state changes that the object goes through, and the side effects from the execution of methods.

**Subtyping in Java requires the base class's properties and methods are available in the subclass.**

However, behavioral subtyping means that not only does a subtype provide all of the methods in the supertype, but it **must adhere to the behavioral specification of the supertype.** This ensures that any assumptions made by the clients about the supertype behavior are met by the subtype.

### 3. Roles 

Let's now look at some rules/techniques concerning method signatures, invariants, preconditions, and postconditions that we can follow and use to ensure we create well-behaved subtypes.

### 3.1. Signature Rule – Method Argument Types

This rule states that **the overridden subtype method argument types can be identical or wider than the supertype method argument types.**

### 3.2. Signature Rule – Return Types

**The return type of the overridden subtype method can be narrower than the return type of the supertype method.**

### 3.3. Signature Rule – Exceptions

**The subtype method can throw fewer or narrower (but not any additional or broader) exceptions than the supertype method.**

This is understandable because when the client code substitutes a subtype, it can handle the method throwing fewer exceptions than the supertype method. However, if the subtype's method throws new or broader checked exceptions, it would break the client code.

Java's method overriding rules already enforce this rule for checked exceptions. However, **overriding methods in Java CAN THROW any RuntimeException** regardless of whether the overridden method declares the exception.

### 3.4. Properties Rule – Class Invariants
A class invariant is an assertion concerning object properties that must be true for all valid states of the object.

### 3.5 Properties Rule – History Constraint

The history constraint states that the **subclass methods (inherited or new) shouldn't allow state changes that the base class didn't allow.**

### 3.6 Methods Rule – Preconditions

A precondition should be satisfied before a method can be executed.**A subtype can weaken (but not strengthen) the precondition for a method it overrides.**


### 3.7 Methods Rule – Postconditions

A postcondition is a condition that should be met after a method is executed.**The subtype can strengthen (but not weaken) the postcondition for a method it overrides.**


### 4. Code Smells

How can we spot a subtype that is not substitutable for its supertype in the real world?

Let's look at some common code smells that are signs of a violation of the Liskov Substitution Principle.

### 4.1 A Subtype Throws an Exception for a Behavior It Can't Fulfill

### 4.2 A Subtype Provides No Implementation for a Behavior It Can't Fulfill

This is a variation of the above code smell. The subtype cannot fulfill a behavior and so it does nothing in the overridden method.

### 4.3 The Client Knows About Subtypes

If the client code needs to use instanceof or downcasting, then the chances are that both the Open/Closed Principle and the Liskov Substitution Principle have been violated.

### 4.4 A Subtype Method Always Returns the Same Value

It depends on the interface, and what the value means, but generally hardcoding what should be a changeable state value of an object is a sign that the subclass is not fulfilling the whole of its supertype and is not truly substitutable for it.


### 5. Conclusion

In this article, we looked at the Liskov Substitution SOLID design principle.

The Liskov Substitution Principle helps us model good inheritance hierarchies. It helps us prevent model hierarchies that don't conform to the Open/Closed principle.

Any inheritance model that adheres to the Liskov Substitution Principle will implicitly follow the Open/Closed principle.

To begin with, we looked at a use case that attempts to follow the Open/Closed principle but violates the Liskov Substitution Principle. Next, we looked at the definition of the Liskov Substitution Principle, the notion of behavioral subtyping, and the rules that subtypes must follow.

Finally, we looked at some common code smells that can help us detect violations in our existing code.


Relateds :
```
 https://www.baeldung.com/java-liskov-substitution-principle 
```

Tags :
```
#java #principle #liskov 
```
