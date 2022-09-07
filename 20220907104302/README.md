# Effective Java Section 3 Item 14

## Consider implementing Comparable
 
 Unlike the other methods discussed in this chapter, the compareTo method is not declared in Object. Rather, it is the sole method in the Comparable interface. It is similar in character to Object’s equals method, except that it permits order comparisons in addition to simple equality comparisons, and it is generic. By implementing Comparable, a class indicates that its instances have a natural ordering. Sorting an array of objects that implement Comparable is as simple as this:
  Arrays.sort(a);


### Method compareTo() : 
Compares this object with the specified object for order. Returns a negative integer, zero, or a positive integer as this object is less than, equal to, or greater
than the specified object.

- The implementor must ensure that sgn(x.compareTo(y)) == -sgn(y.compareTo(x)) for all x and y. (This implies that x.compareTo(y) must throw an exception if and only if y.compareTo(x) throws an exception.)

- The implementor must also ensure that the relation is transitive: (x.compareTo(y) > 0 && y.compareTo(z) > 0) implies x.compareTo(z) > 0.

- Finally, the implementor must ensure that x.compareTo(y) == 0 implies that sgn(x.compareTo(z)) == sgn(y.compareTo(z)), for all z.

- It is strongly recommended, but not required, that (x.compareTo(y) == 0) == (x.equals(y)).

 The first provision says that if you reverse the direction of a comparison between two object references, the expected thing happens: if the first object is less than the second, then the second must be greater than the first; if the first object is equal to the second, then the second must be equal to the first; and if the first object is greater than the second, then the second must be less than the first. The second provision says that if one object is greater than a second and the second is greater than a third, then the first must be greater than the third. The final provision says that all objects that compare as equal must yield the same results when compared to any other object.


### Notes :
One consequence of these three provisions is that the equality test imposed by a compareTo method must obey the same restrictions imposed by the equals contract: reflexivity, symmetry, and transitivity.

Therefore, the same caveat applies:
there is no way to extend an instantiable class with a new value component while preserving the compareTo contract, unless you are willing to forgo the benefits of object-oriented abstraction (Item 10). The same workaround applies, too. If you want to add a value component to a class that implements Comparable, don’t extend it; write an unrelated class containing an instance of the first class. Then provide a “view” method that returns the contained instance. This frees you to implement whatever compareTo method you like on the containing class, while allowing its client to view an instance of the containing class as an instance of the contained class when needed. The final paragraph of the compareTo contract, which is a strong suggestion rather than a true requirement, simply states that the equality test imposed by the compareTo method should generally return the same results as the equals method. If this provision is obeyed, the ordering imposed by the compareTo method is said to be consistent with equals. If it’s violated, the ordering is said to be inconsistent with equals. A class whose compareTo method imposes an order that is inconsistent with equals will still work, but sorted collections containing elements of the class may not obey the general contract of the appropriate collection interfaces (Collection, Set, or Map). This is because the general contracts for these interfaces are defined in terms of the equals method, but sorted collections use the equality test imposed by compareTo in place of equals. It is not a catastrophe if this happens, but it’s something to be aware of. For example, consider the BigDecimal class, whose compareTo method is inconsistent with equals. If you create an empty HashSet instance and then add new BigDecimal("1.0") and new BigDecimal("1.00"), the set will contain two elements because the two BigDecimal instances added to the set are unequal when compared using the equals method. If, however, you perform the same procedure using a TreeSet instead of a HashSet, the set will contain only one element because the two BigDecimal instances are equal when compared using the compareTo method. (See the BigDecimal documentation for details.)



### Summary :

whenever you implement a value class that has a sensible ordering, you should have the class implement the Comparable interface so that its instances can be easily sorted, searched, and used in comparison-based collections. When comparing field values in the implementations of the compareTo methods, avoid the use of the < and > operators. Instead, use the static compare methods in the boxed primitive classes or the comparator construction methods in the Comparator interface.


Tags :
```
#java #comparable #comparator #equals
```

