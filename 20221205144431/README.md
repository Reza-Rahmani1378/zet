# Volatile Keyword in java 

**Volatile keyword is used to modify the value of a variable by different threads. It is also used to make classes thread safe. It means that multiple threads can use a method and instance of the classes at the same time without any problem. The volatile keyword can be used either with primitive type or objects.**

## When to use it?
- You can use a volatile variable if you want to read and write long and double variable automatically.
- It can be used as an alternative way of achieving synchronization in Java.
- All reader threads will see the updated value of the volatile variable after completing the write operation. If you are not using the volatile keyword, different reader thread may see different values.
- It is used to inform the compiler that multiple threads will access a particular statement. It prevents the compiler from doing any reordering or any optimization.
- If you do not use volatile variable compiler can reorder the code, free to write in cache value of volatile variable instead of reading from the main memory.



## Important points

- You can use the volatile keyword with variables. Using volatile keyword with classes and methods is illegal.
- It guarantees that value of the volatile variable will always be read from the main memory, not from the local thread cache.
- If you declared variable as volatile, Read and Writes are atomic
- It reduces the risk of memory consistency error.
- Any write to volatile variable in Java establishes a happen before the relationship with successive reads of that same variable.
- The volatile variables are always visible to other threads.
- The volatile variable that is an object reference may be null.
- When a variable is not shared between multiple threads, you do not need to use the volatile keyword with that variable.

## Example of Volatile Keyword

```java
public class VolatileData {

    private volatile int counter = 0;


    public int getCounter() {
        return counter;
    }

    public void increaseCounter() {
        ++counter;
    }
}

public class VolatileThreadData extends Thread{

    private VolatileData volatileData;

    public VolatileThreadData(VolatileData volatileData) {
        this.volatileData = volatileData;
    }
    @Override
    public void run() {
        int oldData = volatileData.getCounter();

        System.out.println("[Thread " + Thread.currentThread().getId() + "]:" + "Old Value is :" + oldData );

        this.volatileData.increaseCounter();
        int newData = volatileData.getCounter();
        System.out.println("[Thread " + Thread.currentThread().getId() + "]:" + "New Value is :" + newData );
    }

    public static void main(String[] args) throws InterruptedException {
        int numberOfThreads = 2;
        VolatileData volatileDataTest = new VolatileData();
        Thread[] threads = new Thread[numberOfThreads];
        for (int i = 0; i < threads.length; i++) {
            threads[i] = new VolatileThreadData(volatileDataTest);
        }
        for (Thread thread : threads) {
            thread.start();
            thread.join();
        }


    }
}
```

**Related**:
```
#java #volatile #keyword
```
**Links**:
```
https://www.javatpoint.com/volatile-keyword-in-java#:~:text=Volatile%20keyword%20is%20used%20to,with%20primitive%20type%20or%20objects.
```
