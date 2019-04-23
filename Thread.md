## Thread

### 1. 创建线程 

- 继承Thread类(不推荐)
- 实现Runnable接口, 有以下好处
  1. 避免java中单继承的限制
  2. 兼容线程池
  3. 代码可被多个线程共享

### 2. 线程的状态转换 (重点)

![](https://img-blog.csdn.net/20180509145914703?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L09VQ0ZTQg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 3. 守护线程

在Java中有两类线程：User Thread(用户线程)、Daemon Thread(守护线程) 

用个比较通俗的比如，任何一个守护线程都是整个JVM中所有非守护线程的保姆：

只要当前JVM实例中尚存在任何一个非守护线程没有结束，守护线程就全部工作；只有当最后一个非守护线程结束时，守护线程随着JVM一同结束工作。
Daemon的作用是为其他线程的运行提供便利服务，守护线程最典型的应用就是 GC (垃圾回收器)，它就是一个很称职的守护者。

User和Daemon两者几乎没有区别，唯一的不同之处就在于虚拟机的离开：如果 User Thread已经全部退出运行了，只剩下Daemon Thread存在了，虚拟机也就退出了。 因为没有了被守护者，Daemon也就没有工作可做了，也就没有继续运行程序的必要了。 转自 [](https://www.cnblogs.com/ziq711/p/8228255.html)

### 4. 名字和优先级

### 5. 线程常用方法

- wait
- notify
- yield

### 6. 常见面试题

```Java
package com.Lrd.thread;


/*
*   经典面试题目： 建立三个线程，A线程打印10次A，B线程打印10次B,C线程打印10次C，要求线程同时运行，交替打印10次ABC。
*
*   基本思路： 创建第4个线程，控制这三个线程的启动和暂停。
* */
public class printLetterMutliThr1 {
    public static void main(String[] args) {
        PrintLetterRunner printA  = new PrintLetterRunner('A');
        PrintLetterRunner printB  = new PrintLetterRunner('B');
        PrintLetterRunner printC  = new PrintLetterRunner('C');

        Thread a = new Thread(printA);
        Thread b = new Thread(printB);
        Thread c = new Thread(printC);

        a.setDaemon();
        a.start();
        b.start();
        c.start();

        int i=0;
        while (i < 10){
            try {
                printA.printOnce();
                Thread.sleep(100);
                printB.printOnce();
                Thread.sleep(100);
                printC.printOnce();
                Thread.sleep(100);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            i++;
        }
    }
}

class PrintLetterRunner implements Runnable{

    private final Object obj = new Object();
    private char letter;
    private PrintLetterRunner(){}

    public PrintLetterRunner(char letter){this.letter = letter;}

    public void printOnce(){
        synchronized (obj){
            obj.notify();
        }
    }

    @Override
    public void run() {
        synchronized (obj){
            for (;;){
                try {
                    obj.wait();
                    System.out.println(letter);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        }
    }
}
```

