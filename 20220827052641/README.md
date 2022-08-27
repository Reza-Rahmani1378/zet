# Java Eeffective Item 7 Eliminate obsolete object references


## Notes :

 Memory leaks in garbage-collected languages (more properly known as unintentional object retentions) are insidious. If an object reference is unintentionally retained, not only is that object excluded from garbage collection, but so too are any objects referenced by that object, and so on. Even if only a few object references are unintentionally retained, many, many objects may be prevented from being garbage collected, with potentially large effects on performance. The fix for this sort of problem is simple: null out references once they become obsolete. In the case of our Stack class, the reference to an item becomes obsolete as soon as it’s popped off the stack. An added benefit of nulling out obsolete references is that if they are subsequently dereferenced by mistake, the program will immediately fail with a NullPointerException, rather than quietly doing the wrong thing.

 **Nulling out object references should be the exception rather than the norm.** The best way to eliminate an obsolete reference is to let the variable that contained the reference fall out of scope.

 Generally speaking, whenever a class manages its own memory, the programmer should be alert for memory leaks. Whenever an element is freed, any object references contained in the element should be nulled out.

 Another common source of memory leaks is caches.

 A third common source of memory leaks is listeners and other callbacks.


Tags :
```
#java #objects #garbage #reference 
```

