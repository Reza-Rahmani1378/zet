# Java 8 StringJoiner


## 1. Introduction

StringJoiner is a new class added in Java 8 under java.util package. Simply put, **it can be used for joining Strings making use of a delimiter, prefix, and suffix.**


## 2. Adding Elements
```java
@Test
public void whenAddingElements_thenJoinedElements() {
    StringJoiner joiner = new StringJoiner(",", PREFIX, SUFFIX);
    joiner.add("Red")
      .add("Green")
      .add("Blue");

    assertEquals(joiner.toString(), "[Red,Green,Blue]");
}
```

## 3. Construction 

**To construct an instance of StringJoiner, we need to mention the delimiter.**

```java
@Test
public void whenEmptyJoinerWithoutPrefixSuffix_thenEmptyString() {
    StringJoiner joiner = new StringJoiner(",");

    assertEquals(0, joiner.toString().length());
}
```
**A Joiner without prefix and suffix returns an empty String whereas joiner with prefix and suffix returns a String containing both prefix and suffix.** We can change the default String returned by using setEmptyValue():

```java 
@Test
public void whenEmptyJoinerWithEmptyValue_thenDefaultValue() {
    StringJoiner joiner = new StringJoiner(",");
    joiner.setEmptyValue("default");

    assertEquals(joiner.toString(), "default");
}

@Test
public void whenEmptyJoinerWithPrefixSuffixAndEmptyValue_thenDefaultValue() {
    StringJoiner joiner = new StringJoiner(",", PREFIX, SUFFIX);
    joiner.setEmptyValue("default");

    assertEquals(joiner.toString(), "default");
}
```
## 4. Merge Joiners
We can merge two joiners using merge(). It adds the contents of the given StringJoiner **without prefix and suffix as the next element.**
```java
@Test
public void whenMergingJoiners_thenReturnMerged() {
    StringJoiner rgbJoiner = new StringJoiner(
      ",", PREFIX, SUFFIX);
    StringJoiner cmybJoiner = new StringJoiner(
      "-", PREFIX, SUFFIX);

    rgbJoiner.add("Red")
      .add("Green")
      .add("Blue");
    cmybJoiner.add("Cyan")
      .add("Magenta")
      .add("Yellow")
      .add("Black");

    rgbJoiner.merge(cmybJoiner);

    assertEquals(
      rgbJoiner.toString(),
      "[Red,Green,Blue,Cyan-Magenta-Yellow-Black]");
}
```

## 5. Stream API
```java
@Test
public void whenUsedWithinCollectors_thenJoined() {
    List<String> rgbList = Arrays.asList("Red", "Green", "Blue");
    String commaSeparatedRGB = rgbList.stream()
      .map(color -> color.toString())
      .collect(Collectors.joining(","));

    assertEquals(commaSeparatedRGB, "Red,Green,Blue");
}
```

**Related** :
```
#java8 #StringJoiner 
```

**Links**:
```
https://www.baeldung.com/java-string-joiner
```
