用锁的最佳实践
Doug Lea《Java 并发编程:设计原则与模式》一书中， 推荐的三个用锁的最佳实践，它们分别是:
1. 永远只在更新对象的成员变量时加锁
2. 永远只在访问可变的成员变量时加锁
3. 永远不在调用其他对象的方法时加锁

KK 总结-最小使用锁: 
1、降低锁范围:锁定代码的范围/作用域
2、细分锁粒度:讲一个大锁，拆分成多个小锁


思考一下: 多个线程之间怎么相互协作? 前面讲到的: 1、wait/notify 2、Lock/Condition 可以作为简单的协作机制。
但是更复杂的，需要这些线程 满足某些条件(数量，时间)。

更复杂的应用场景，比如
- 我们需要控制实际并发访问资源的并发数量
- 我们需要多个线程在某个时间同时开始运行
- 我们需要指定数量线程到达某个状态再继续处理

## countDownLatch事例

```
public static class CountDownLatchTask implements Runnable {
private CountDownLatch latch;
public CountDownLatchTask(CountDownLatch latch) { } this.latch=latch;
@Override
public void run() {
Integer millis = new Random().nextInt(10000); try {
TimeUnit.MILLISECONDS.sleep(millis);
this.latch.countDown(); System.out.println("我的任务OK了:"+Thread.currentThread().getName());
} catch (Exception e) { } 
```

```
/ 使用示例
public static void main(String[] args)
throws Exception {
int num = 100; CountDownLatch latch = new
CountDownLatch(num); List<CompletableFuture> list = new
ArrayList<>(num);
for (int i = 0; i < num; i++) {
CompletableFuture<Void> future = CompletableFuture.runAsync(
new CountDownLatchTask(latch)); } list.add(future);
latch.await();
for (CompletableFuture future : list) { } } fut
```

![](../img/2021-11-27-java-concurrency/futureTask.png)

## 加锁需要考虑的问题
1. 粒度
2. 性能
3. 重入
4. 公平
5. 自旋锁(spinlock)
6. 场景: 脱离业务场景谈性能都是耍流氓

## 线程间协作与通讯

1. 线程间共享:
- static/实例变量(堆内存)
- Lock
- synchronized
2. 线程间协作:
- Thread#join()
- Object#wait/notify/notifyAll • Future/Callable
- CountdownLatch
- CyclicBarrier
- ExChanger


## 进程间协作与通讯
1. 分布式锁