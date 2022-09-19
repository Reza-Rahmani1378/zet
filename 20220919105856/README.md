# Spring Boot Async Executor Management with ThreadPoolTaskExecutor

1. **Challenge** : In Trendyol, we are developing a micro service project for integrate some third party systems. In this integration, we should consume some pageable api’s in every two hours. In this progress micro service will consume api over than 200.000 times. Every api call using resources and managing these progress going to complex. We can not consume api in single thread, because every 2 hour starting new scheduler and progress should finish immediately. In this way we are choosing to use Asynchronous programming for this progress.
In fact looks like simple to call every api request in asynchronous, but there is a threshold. If we start to consume over than 200.000 request in same time, every thread consume resources and if resources not enough system will block. In dockerized application workflow, your micro service container will down and start again when system block and not responding. This mean you will lose the state of your application and you should start progress again. Because of these you should make your asynchronous threads scaleable and non blocking.


2. **Summary** : In this article, i will try to explain important points of managing Spring Boot **@Async** feature with **ThreadPoolTaskExecutor.**

Enabling to asynchronous functionality in Spring Boot is very easy with using @EnableAsync annotation over any of Spring Boot configuration class. But managing is async not easy like this, you should analyze your application of how many threads will be running at same time and scalability. After that you should define an Executor (java.util.concurrent.Executor) implementation for manage your @Async functions.

3. **Overview** : Sample of ThreadPoolTaskExecutor definition is like following picture. We will follow this definition in this article.

![image](https://miro.medium.com/max/700/1*FmGCytv1eJzV6SqMw9jfPA.png)

ThreadPoolTaskExecutor contains following concepts:

- **Core Pool Size** :Core pool size is defines minimum paralel threads can run at same time. In our sample, CORE_POOL_SIZE = 75 and this mean, our application can increase paralel running threads up to 75. If our application need more thread over than 75, new threads will be added into queue.

- **Queue Capacity** :  Queue is using when all core pool are filled. Threads will be scalable to maximum pool size when queue is full. In our application, let’s imagine 75 threads running at same time and also 75 threads more in queue. Totally we have 150 threads. Pool size will be increased until maximum pool size for each thread over 150.

- **Maximum Pool Size** : Maximum pool size defines maximum parallel threads can run at same time. In our sample MAX_POOL_SIZE = 100 and this mean, our application can be increase to 100 parallel running threads when queue is full.

After all, we should decide what will happen to more thread when maximum pool and queue is full.
Some approach is define queue is Integer.MAX_VALUE, but i’m not suggested this approach. Maximum defined queue is means never will be filled and your application will never scale from core pool size to maximum pool size.
Also some other approach is core pool and maximum pool size set same value and using queue maximum. This means fixed size thread pool without scalability. You can not decide your cpu and memory utilization.

Now let’s decide what will happen to more threads when maximum pool and queue is full. In Spring’s default , threads will be rejected with ThreadPoolExecutor.AbortPolicy and you lose new threads. For scalable application i’m suggested to use ThreadPoolExecutor.CallerRunsPolicy. This policy provides to us scalable queue when maximum pool is filled.

ThreadPoolTaskExecutor has following policies definitions;

**ThreadPoolExecutor.AboutPolicy** : Rejecting the thread with throwing RejectedExecutionException. You will lose the thread.
**ThreadPoolExecutor.CallerRunsPolicy** : The thread invokes itself on rejected pool. You will not lose the thread. This policy like increasing queue capacity. You can manage your application with this policy.
**ThreadPoolExecutor.DiscardPolicy** : The thread will be discard. You will lose the thread.
**ThreadPoolExecutor.DiscardOldestPolicy** : This policy discards the oldest unhandled request. You will lose some threads inside queue.


Tags :
```
#java #spring-boot #policy #thread #executor #task
```

Related :
```
https://medium.com/trendyol-tech/spring-boot-async-executor-management-with-threadpooltaskexecutor-f493903617d
```
