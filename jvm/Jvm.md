java 刚启动后有几个线程
```java
class Test {
  public static void main(String[] args){
    TimeUnit.MINUTES.sleep(5000); 
  }
}
```

运行以后，jps，jstack。查看线程栈
```
Full thread dump Java HotSpot(TM) 64-Bit Server VM (25.131-b11 mixed mode):

"Attach Listener" #11 daemon prio=9 os_prio=31 tid=0x00007fb6ec04a800 nid=0x4a07 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"Service Thread" #10 daemon prio=9 os_prio=31 tid=0x00007fb6e9844800 nid=0x4003 runnable [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"C1 CompilerThread3" #9 daemon prio=9 os_prio=31 tid=0x00007fb6e9827000 nid=0x3e03 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"C2 CompilerThread2" #8 daemon prio=9 os_prio=31 tid=0x00007fb6ea80d800 nid=0x3c03 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"C2 CompilerThread1" #7 daemon prio=9 os_prio=31 tid=0x00007fb6ea80d000 nid=0x4303 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"C2 CompilerThread0" #6 daemon prio=9 os_prio=31 tid=0x00007fb6e9826800 nid=0x3b03 waiting on condition [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"Monitor Ctrl-Break" #5 daemon prio=5 os_prio=31 tid=0x00007fb6e9824000 nid=0x3903 runnable [0x000070000d818000]
   java.lang.Thread.State: RUNNABLE
        at java.net.SocketInputStream.socketRead0(Native Method)
        at java.net.SocketInputStream.socketRead(SocketInputStream.java:116)
        at java.net.SocketInputStream.read(SocketInputStream.java:171)
        at java.net.SocketInputStream.read(SocketInputStream.java:141)
        at sun.nio.cs.StreamDecoder.readBytes(StreamDecoder.java:284)
        at sun.nio.cs.StreamDecoder.implRead(StreamDecoder.java:326)
        at sun.nio.cs.StreamDecoder.read(StreamDecoder.java:178)
        - locked <0x000000076ac835b0> (a java.io.InputStreamReader)
        at java.io.InputStreamReader.read(InputStreamReader.java:184)
        at java.io.BufferedReader.fill(BufferedReader.java:161)
        at java.io.BufferedReader.readLine(BufferedReader.java:324)
        - locked <0x000000076ac835b0> (a java.io.InputStreamReader)
        at java.io.BufferedReader.readLine(BufferedReader.java:389)
        at com.intellij.rt.execution.application.AppMainV2$1.run(AppMainV2.java:64)

"Signal Dispatcher" #4 daemon prio=9 os_prio=31 tid=0x00007fb6e9823000 nid=0x4603 runnable [0x0000000000000000]
   java.lang.Thread.State: RUNNABLE

"Finalizer" #3 daemon prio=8 os_prio=31 tid=0x00007fb6e9809000 nid=0x3403 in Object.wait() [0x000070000d612000]
   java.lang.Thread.State: WAITING (on object monitor)
        at java.lang.Object.wait(Native Method)
        - waiting on <0x000000076ab08ec8> (a java.lang.ref.ReferenceQueue$Lock)
        at java.lang.ref.ReferenceQueue.remove(ReferenceQueue.java:143)
        - locked <0x000000076ab08ec8> (a java.lang.ref.ReferenceQueue$Lock)
        at java.lang.ref.ReferenceQueue.remove(ReferenceQueue.java:164)
        at java.lang.ref.Finalizer$FinalizerThread.run(Finalizer.java:209)

"Reference Handler" #2 daemon prio=10 os_prio=31 tid=0x00007fb6ea005000 nid=0x3203 in Object.wait() [0x000070000d50f000]
   java.lang.Thread.State: WAITING (on object monitor)
        at java.lang.Object.wait(Native Method)
        - waiting on <0x000000076ab06b68> (a java.lang.ref.Reference$Lock)
        at java.lang.Object.wait(Object.java:502)
        at java.lang.ref.Reference.tryHandlePending(Reference.java:191)
        - locked <0x000000076ab06b68> (a java.lang.ref.Reference$Lock)
        at java.lang.ref.Reference$ReferenceHandler.run(Reference.java:153)

"main" #1 prio=5 os_prio=31 tid=0x00007fb6ec001800 nid=0x2603 waiting on condition [0x000070000caf1000]
   java.lang.Thread.State: TIMED_WAITING (sleeping)
        at java.lang.Thread.sleep(Native Method)
        at java.lang.Thread.sleep(Thread.java:340)
        at java.util.concurrent.TimeUnit.sleep(TimeUnit.java:386)
        at Test.main(Test.java:9)

"VM Thread" os_prio=31 tid=0x00007fb6eb807000 nid=0x4f03 runnable 

"GC task thread#0 (ParallelGC)" os_prio=31 tid=0x00007fb6ec800800 nid=0x1907 runnable 

"GC task thread#1 (ParallelGC)" os_prio=31 tid=0x00007fb6e9800000 nid=0x1a03 runnable 

"GC task thread#2 (ParallelGC)" os_prio=31 tid=0x00007fb6ed801800 nid=0x2b03 runnable 

"GC task thread#3 (ParallelGC)" os_prio=31 tid=0x00007fb6ec00b800 nid=0x2d03 runnable 

"GC task thread#4 (ParallelGC)" os_prio=31 tid=0x00007fb6ec00c000 nid=0x2e03 runnable 

"GC task thread#5 (ParallelGC)" os_prio=31 tid=0x00007fb6eb804800 nid=0x2f03 runnable 

"GC task thread#6 (ParallelGC)" os_prio=31 tid=0x00007fb6ea805800 nid=0x5203 runnable 

"GC task thread#7 (ParallelGC)" os_prio=31 tid=0x00007fb6ea806800 nid=0x5103 runnable 

"VM Periodic Task Thread" os_prio=31 tid=0x00007fb6ea051000 nid=0x5503 waiting on condition 

JNI global references: 22
```
可以看出线程有几下几类
Signal Dispatcher:该线程是jvm启动的时候就启动了，接收信号。
attach Listener：这个与attach机制有关，比如jstack，dump等都与此有关。可参考 https://blog.csdn.net/u010725670/article/details/50630689

Service Thread：暂时还不清楚

C1 CompilerThread3
C2 CompilerThread2
C2 CompilerThread1
C2 CompilerThread0: 与配置的参数 CICompilerCount有关，启动时，该参数配置的为4，C1类型的占1/3，向下取整。

Monitor Ctrl-Break：
Finalizer：这个线程也是在main线程之后创建的，其优先级为10，主要用于在垃圾收集前，调用对象的finalize()方法
Reference Handler：VM在创建main线程后就创建Reference Handler线程，其优先级最高，为10，它主要用于处理引用对象本身（软引用、弱引用、虚引用）的垃圾回收问题
main：这个都懂
VM Thread
GC task thread#[0-7]：进行gc
VM Periodic Task Thread:


