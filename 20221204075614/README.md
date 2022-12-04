# Java 8 StringJoiner

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
