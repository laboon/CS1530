## Dealing with Concurrency

### What Is A Thread?  Why Do We Use Them?

* Like a process within a process (a lightweight process); a flow of execution inside a program.
  * Processes are self-contained execution environments, including allocated memory space
  * Process communicate via IPC (inter-process communication) measures such as pipes and sockets
  * Not an application - an application may be many different processes (e.g. Chrome tabs)
  * Every process has at least one thread
  * However, threads can share state (access/modify same variables, for instance)
  * Super-duper efficient!

* Let's say you have two threads operating on a single processor.
  * Thread1 operations indicated by 1's, Thread2 by 2's
```
11111       111           1111
     2222222   22222222222    2222
time -------------------------------->

```
* Of course, there are also context switch costs.  More efficient to run in a single thread on a single processor (if you can)
  * OK, then why use threads?  Well, what about multi-core, multi-proc machines?
```
1111111111111111111111111111111111111
2222222222222222222222222222222222222
time -------------------------------->
```
  * Threads often only need to be listening or polling for something
  * Makes sense logically to keep concerns separate
    * Do you really want to manually add places for garbage collection in in your code?

### How Do Threads Work in Java?

* There are two kinds of threads
  * Green threads: controlled by the runtime library or virtual machine
  * OS threads: controlled by the operating system
  * Unless you are using Java 1.1, you are probably using OS threads

* There are lots of threads in ANY Java program, most of which you are not aware of
  * Garbage collection
  * Signal listener
  * Profiling listener

* Threads are Runnables, they have a .run() method
  * Start them by calling .start(), which executes .run() on a new thread
  * Note that there are other Runnable things other than threads!
  * Theoretically, you could just extend Thread instead of making a thread and passing it a Runnable - this is frowned upon (much less flexible)
  * Threads can sleep with `Thread.sleep(n)` where n is number of milliseconds to sleep
  * Threads can be woken up with interruptions - call the interrupt() method on a Thread object - ultra-simple inter-thread communications
  * You can use thread.join() to pause execution until thread is done
  * Remember that you always have one user thread (main!) to start with

```java
public class ThreadTest {

    public static void main(String args[]) {
        Thread t1 = new Thread() {
            public void run() {
                for (int j=0; j < 10; j++) {
                    System.out.println("T1> " + j);
                    try { 
                        Thread.sleep(10);
                    } catch (Exception e) {} 
                }
                 
            } 
        };
        Thread t2 = new Thread() {
            public void run() {
            	    int foo = 1;
                for (int j=0; j < 10; j++) {
                    System.out.println("T2> " + j);
                    
                    for (int k=0; k < 1000000; k++) {
                    	   foo += (k % 6) - 3; 
                    }
                }
                  
            } 
        }; 
        t1.start();    
        t2.start();
        int bar = 1;
        for (int j=0; j < 10; j++) {
            System.out.println("MAIN> " + j);
            for (int k=0; k < 1000000; k++) {
         	   bar = bar - 3 + (k % 7); 
            }
        }

    }

}
```

### What Problems Come With Using Threads?

* Race Conditions
  * A situation where the result depends on the order of thread execution
  * Classic example - two threads incrementing a variable
```java
private int _foo = 0;

public void incrementFoo() {
    _foo++;
}
```  
  * Remember that _foo++ is really three operations!
    * Get value of foo and put in temp variable
    * Add one to temp variable
    * Set value of foo to value of temp variable
  * Thread1 gets value of foo = 0, puts in temp variable
  * Context switch - Thread2 gets value of foo = 0, puts in temp variable
  * Context switch - Thread1 adds 1 to temp, puts it in _foo (now == 1)
  * Context switch - Thread2 adds 1 to temp, puts it in _foo (now == 1)
  * Should have been 2!
  * This is a critical section - a part of the code that should not be concurrently executed by two different threads.  
  * Requires mutual exclusion of access
  * Another way of thinking about it, atomic access
    * Atomic access - from a logical perspective, everything happens at once
  * `volatile` variables - specify that a value may change between accesses, even if not in this thread - prevents optiization

* Quick way to avoid - use synchronized
```java
private int _foo = 0;

public synchronized void incrementFoo() {
    _foo++;
}
``` 

* You will be locking on the object (__this__) by doing this

* You can lock on the class - ensuring that no instances of the object call this method on another thread by using static
```java
private static int _foo = 0;

public synchronized void incrementFoo() {
    _foo++;
}
``` 

* If you don't care about the whole method, or want to lock on a different object, you can synchronize in a block
```java
private int _foo = 0;

public  void incrementFoo() {
    System.out.println("Debug info - Don't care about synchronizing this at all");
    int i = 7;
    i += 10;
    System.out.println(i); // No reliance on shared variables, no need to sync
    synchronized(this) {
        _foo++;
    }
}
``` 

* Another way to avoid it is by using the Atomic* classes
```java
private AtomicInteger _foo = new AtomicInteger(0);

public void incrementFoo() {
    int throwaway = _foo.incrementAndGet();
}
``` 

* Deadlock
  * Assume that a thread needs two resources to do its work, r1 and r2
    * Let's say r1 is a file and r2 is a printer connection
  * Thread1 and Thread2 want to print
  * Thread1 wants to print, so it grabs r1
  * Thread2 wants to print, so it grabs r2
  * Thread1 thinks, "ahh, just need r2, but it's in use.  It's cool, I'll wait forever for it."
  * Thread2 thinks, "ahh, just need r1, but it's in use.  It's cool, I'll wait forever for it."
  * Program is deadlocked!

  * How to avoid?
    * Always have a specific order of resource getting (lock hierarchy)
    * Use timeouts

* Livelock
  * Like deadlock, but stuff happening - code is executing but never progresses
    * In previous example, Thread1 says OK, I'll give up r1.
    * Thread2 gives up r2.
    * Thread1 sees r2 is free, grabs it.
    * Thread2 sees r1 is free, grabs it.
    * Thread1 gives up r2.
    * Thread2 gives up r1.
    * Thread1 sees r1 is free, grabs it.
    * Thread2 sees r2 is free, grabs it.
    * Repeat ad infinitum.
  * How to avoid?
    * Lock hierarchies help
    * Add some randomness

* Starvation
  * Thread can never get to a resource it needs =(
  * For example, if another thread never gives up its lock on a printer
  * Or a thread is not returned to a pool
  * How to avoid?
    * Make sure you give up resources when done, or add a timeout to return to pool
    * Allow threads to do work without resources

### Testing
  * It's really hard, especially in unit tests
  * Oftentimes, errors can be "swallowed up" because they are happening in another thread - all you see is a timeout or deadlock
  * You can check aspects of it, such as ensuring that a state is locked
  * Systems-level tests
    * Going to be coarse-grained
    * Will help you find problems, still need to track them down
  * Stress tests
    * Run multiple threads
    * Tune the stress test until you get it to fail consistently
    * Make test pass by modifying code
  
### How To Avoid Threading Problems In General

* If you don't need to use threads, don't.

* If you do have to...
  * Use already-existing frameworks (e.g. AtomicObject, java.util.concurrent stuff, ConcurrentHashMap, etc.)
  * Start baking in concurrency at beginning of development, not the end
  * Design for concurrency
  * Avoid mutable state!  
  * Make variables final!
  * Share only when necessary!
  * Is Java the right language to be doing this in?  
    * Erlang, Clojure, etc.?

### Further Reading

* Read _Java Concurrency in Practice_ by Brian Goetz.