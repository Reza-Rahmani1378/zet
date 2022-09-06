# Effective Java Section 3 Item 11

## Always override hashCode when you override equals.

**You must override hashCode in every class that overrides equals.**If you fail to do so, your class will violate the general contract for hashCode, which will prevent it from functioning properly in collections such as HashMap and HashSet.


## Here is the contract, adapted from the Object specification :

- When the hashCode method is invoked on an object repeatedly during an execution of an application, it must consistently return the same value, provided no information used in equals comparisons is modified. This value need not remain consistent from one execution of an application to another.

- If two objects are equal according to the equals(Object) method, then calling hashCode on the two objects must produce the same integer result.

- If two objects are unequal according to the equals(Object) method, it is not required that calling hashCode on each of the objects must produce distinct results. However, the programmer should be aware that producing distinct results for unequal objects may improve the performance of hash tables.


** The key provision that is violated when you fail to override hashCode is the second one: equal objects must have equal hash codes.**


## Here is a simple recipe for implements hashCode method :

1. Declare an int variable named result, and initialize it to the hash code c for the first significant field in your object, as computed in step 2.a.

2. For every remaining significant field f in your object, do the following:

 a. Compute an int hash code c for the field:

  i. If the field is of a primitive type, compute Type.hashCode(f), where Type is the boxed primitive class corresponding to f’s type.

  ii. If the field is an object reference and this class’s equals method compares the field by recursively invoking equals, recursively invoke hashCode on the field. If a more complex comparison is required, compute a “canonical representation” for this field and invoke hashCode on the canonical representation. If the value of the field is null, use 0.

  iii. If the field is an array, treat it as if each significant element were a separate field. That is, compute a hash code for each significant element by applying these rules recursively, and combine the values per step 2.b. If the array has no significant elements, use a constant, preferably not 0. If all elements are significant, use Arrays.hashCode.

 b. Combine the hash code c computed in step 2.a into result as follows:

  ```
  result = 31 * result + c;
  ```
3. Return result.

When you are finished writing the hashCode method, ask yourself whether equal instances have equal hash codes.


##Notes :

-  You may exclude derived fields from the hash code computation. In other words, you may ignore any field whose value can be computed from fields included in the computation. You must exclude any fields that are not used in equals comparisons, or you risk violating the second provision of the hashCode contract.

- **Do not be tempted to exclude significant fields from the hash code computation to improve performance.**



##Summary :

you must override hashCode every time you override equals, or your program will not run correctly. Your hashCode method must obey the general contract specified in Object and must do a reasonable job assigning unequal hashcodes to unequal instances. This is easy to achieve, if slightly tedious, using the recipe on page 51. As mentioned in Item 10, the AutoValue framework provides a fine alternative to writing equals and hashCode methods manually, and IDEs also provide some of this functionality.


Tags :
```
#java #hashCode
```

