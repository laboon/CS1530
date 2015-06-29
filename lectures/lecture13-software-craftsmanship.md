## Software Craftsmanship

* As a software engineer, you are not an assembly-line worker.
  * Hard to quantify the work you do
  * Different every time
  * Sometimes managers won't understand what you are doing
  * Being great is up to you

* Three virtues of a programmer (from Larry Wall)
  1. Laziness: The quality that makes you go to great effort to reduce overall energy expenditure. It makes you write labor-saving programs that other people will find useful and document what you wrote so you don't have to answer so many questions about it.
  2. Impatience: The anger you feel when the computer is being lazy. This makes you write programs that don't just react to your needs, but actually anticipate them. Or at least pretend to.
  3. Hubris: The quality that makes you write (and maintain) programs that other people won't want to say bad things about.

* But actually, one of the most important things is intellectual humility
* “True humility is not thinking less of yourself; it is thinking of yourself less.”  -C.S. Lewis, Mere Christianity
* Learning is humility, as it means you are admitting that there are things you don't know
* Humility is also intellectual honesty
  * Don't pretend to be an expert when you're not
  * Readily admit your mistakes
    * Don't be that person on Facebook who ignores Snopes links
  * Don't ignore compiler warnings
  * Be realistic in your status reports and estimates
    * UPOD - Under-promise, over-deliver
    * Also be prepared to fight back.  Estimating is hard, but programmers are better than managers at it.
  * Don't be afraid of deleting code you wrote

* This field is changing very quickly.
  * Read books.  Read blog posts.  Read Hacker News. (hopefully in that order)
  * Meet with other programmers
  * Learn to give talks
  * 30% or less of your time as a programmer will be spent with you programming alone
    * Pair programming, meetings, designing, discussions, whiteboarding, answering questions, etc.
  * This is something that can be developed!  You are not a "born talker".
    * My first performance review: "needs to learn to speak up, never wants to give presentations"

### Themes in Software Craftsmanship

* Reducing complexity
  * Dijkstra wrote in "The Humble Programmer" that the main problem with software engineering is developing programs which are "intellectually manageable" (https://www.cs.utexas.edu/~EWD/transcriptions/EWD03xx/EWD340.html)
  * This guy was a programmer before programmer was recognized as a job; if he was having trouble managing complexity in the '70s, imagine how much worse it is now!
  * Let's imagine a simple Java program:

```java
public class Foo
    public static void main(String args[]) {
       int i = 1 + 1;
       System.out.print("1 + 1 is: ");
       System.out.println(i);
    }
}
```
  * Now let's get down into complexity:
    * Running on a virtual machine, in protected memory, on an operating system
    * Using multiple library functions (java.lang)
    * Being JITted
    * Garbage collection thread running
    * Signal thread running
    * Display - sending data using VT100 commands to a virtualized terminal, with display controlled by the operating system
    * Just typing it in to run - do you know how your keyboard works?  How the terminal accepts characters?  How it displays them?  How your shell interprets commands?
    * How does arithmetic work? (Principia Mathematica)
  * So how to avoid complexity?
    * Proper abstraction - do you really care how the keyboard works?
    * Carefully defined interfaces
    * Avoiding global mutable state
    * Avoiding deep hierarchies
    * Avoiding deep nesting
    * Using a well-defined code style guide
    * Use conventions, "convention over configuration" in Rails world
    * Routines/functions should be short ( < 10 lines)
    * Define how things will work
  * Abstraction is one of the most important things you can do.  Programming at the levels we do today would not be possible without proper abstraction.

* Pick Your Process / Architecture
  * Process and architecture matter quite a bit!  More than you would think!
  * There are always trade-offs.
    * What kind of process would you use for?
      * Doing something for fun to try out a new language
      * Project with very well-defined requirements, loose deadline
      * Project with strict deadline, requirements very loose
    * What kind of architecture would you use for?
      * Data comes in, data goes out
      * System with one finished product, but lots of processes working on it
      * Game where you click the mouse to do things

* Avoid premature optimization
  * "Premature optimization is the root of all evil"

* Write programs for people first, computers second
  * Programmer time is more expensive than people time... this isn't 1958
  * Read "Hackers: Heroes of the Computer Revolution", and especially about the TX-0
    * Three million dollars, 64 kilobytes of memory, oscilloscope
    * Four instructions - Store, Add, Conditional Branch, Operate
    * At this point, yes, computer time was more expensive than programmer time
  * Making code readable by humans means increased:
    * Comprehensibility
    * Reviewability
    * Fewer errors
    * Easier debugging
    * Less development time
    * Better external and internal quality
    * Easier to modify in the future

* Follow Conventions

* Abstractions - program to the right level
  * Machine Code
  * Programming Language Structure
  * Implementation structures
  * Low-level Domain structures
  * High-level domain structures (DSLs if possible and if language supports)

* Software engineering is neither an art nor a science
  * It's not really entirely engineering, either
  * Tread carefully, iterate repeatedly, be careful of mistakes
  * EXPERIMENT!  EXPLORE!  TRY THINGS!
    * I know of nobody who I respect as an engineer who doesn't find it fun
    * This doesn't mean that you need to spend all of your waking moments programming

* Thou Shalt Rend Software and Religion Asunder
  * Avoid falling for cult leaders
  * Be aware of several different programming languages / paradigms / approaches
    * Imperative
    * Object-oriented
    * Procedural
    * Functional
    * Logical
    * Stack-based
    * Declarative

* Remember that as a software engineer, you are a professional
  * Keep ethics in mind
  * Act as a professional
    * This doesn't mean a suit and tie, it means respect people
  * Professionals care about what they do
  
