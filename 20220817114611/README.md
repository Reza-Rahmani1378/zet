# MapStruct - Using expression

MapStruct allows to call a conversion method for customized logic. We can use expression to achieve the same where we can pass any java object and call its method to do the conversion.


**Syntax** :
```
@Mapping(target = "target-property",
   expression = "java(target-method())")

```
Here :
 
 * **target-property** − the property for which we are doing the mapping.

 * **expression** − mapper will call the java method written in the expression.

 * **target-method** − target-method is the method to be called. In case method is present in different class, use new class-name.target-method().


Related : 
```
 * <https://www.tutorialspoint.com/mapstruct/mapstruct_using_expression.htm>
```

Tags :
```
#java #mapstruct #mapping #expression 
```
