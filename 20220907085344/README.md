# Effective java Section 3 Item 13

The Cloneable interface was intended as a mixin interface (Item 20) for classes to advertise that they permit cloning. Unfortunately, it fails to serve this purpose.
Its primary flaw is that it lacks a clone method, and Object’s clone method is protected. You cannot, without resorting to reflection (Item 65), invoke clone on an object merely because it implements Cloneable. Even a reflective invocation may fail, because there is no guarantee that the object has an accessible clone method.

**Despite this flaw and many others, the facility is in reasonably wide use, so it pays to understand it.**


### what does Cloneable do, given that it contains no methods?

**if a class implements Cloneable, Object’s clone method returns a field-by-field copy of the object; otherwise it throws CloneNotSupportedException.**

**in practice, a class implementing Cloneable is expected to provide a properly functioning public clone method.**
In order to achieve this, the class and all of its superclasses must obey a complex, unenforceable, thinly documented protocol. The resulting mechanism is fragile, dangerous, and extralinguistic: **it creates objects without calling a constructor.**

###Note :
but note that **immutable classes should never provide a clone method** because it would merely encourage wasteful copying.


**In effect, the clone method functions as a constructor; you must ensure that it does no harm to the original object and that it properly establishes invariants on the clone.** In order for the clone method on Stack to work properly, it must copy the internals of the stack. The easiest way to do this is to call clone recursively on the elements array:
// Clone method for class with references to mutable state
@Override public Stack clone() {
	try {
		Stack result = (Stack) super.clone();
		result.elements = elements.clone();
		return result;
} catch (CloneNotSupportedException e) {
	throw new AssertionError();
	}
}


**The Cloneable architecture is incompatible with normal use of final fields referring to mutable objects.**

**A better approach to object copying is to provide a copy constructor or copy factory.**


### Summary :

The copy constructor approach and its static factory variant have many advantages over Cloneable/clone: they don’t rely on a risk-prone extralinguistic object creation mechanism; they don’t demand unenforceable adherence to thinly documented conventions; they don’t conflict with the proper use of final fields; they don’t throw unnecessary checked exceptions; and they don’t require casts. Furthermore, a copy constructor or factory can take an argument whose type is an interface implemented by the class. For example, by convention all general-purpose collection implementations provide a constructor whose argument is of type Collection or Map. Interface-based copy constructors and factories, more properly known as conversion constructors and conversion factories, allow the client to choose the implementation type of the copy rather than forcing the client to accept the implementation type of the original. For example, suppose you have a HashSet, s, and you want to copy it as a TreeSet. The clone method can’t offer this functionality, but it’s easy with a conversion constructor: new TreeSet<>(s). Given all the problems associated with Cloneable, new interfaces should not extend it, and new extendable classes should not implement it. While it’s less harmful for final classes to implement Cloneable, this should be viewed as a performance optimization, reserved for the rare cases where it is justified (Item 67). As a rule, copy functionality is best provided by constructors or factories. A notable exception to this rule is arrays, which are best copied with the clone method.


Tags : 
```
#java #cloneable #copy_constructor #immutable

```

