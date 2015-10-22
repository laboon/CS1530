## Object-Oriented Analysis and Design

### Unified Modeling Language (UML)
1. What Is It?
  1. Developed in mid-90s, currently on UML 2.4.  Was not the first OO modeling system but most popular.
  2. Started off as a way to model object-oriented architectures, now used for much more
  3. Static vs Dynamic views
    1. Static view - how the classes go together, structures, attributes, etc.  You can see this by looking at your code in a text editor/IDE and seeing how things fit together.
    2. Dynamic view - How the system works when it is running - which classes call which ones WHEN.  This can be seen by running the code (or mentally doing so)
    3. If you can make a distinction based on time, it's a dynamic view
  3. Can sometimes be used for code generation
    * Honestly, though, I've never heard of this working out well in real life.
  4. Really complex.  Tries to cover every concept of software development.
  5. Benefits: provides a common symbology. 
  6. Depending on domain, will spend more/less time on design
2. Class Diagram (static)
  1. Classes are boxes with three parts
    1. Name
    2. Attributes
    3. Methods
  2. For attributes and methods, can use 
    1. `+` for public
    2. `-` for private
    3. `#` for protected
  3. Classes are related to each other via links
    1. Generalization 
      1.  empty arrow, usually superclass on top, subclass on bottom
      2.  "is-a" relationship
      3.  e.g. A Duck "is-a" Bird, a Cockatiel "is-a" Bird
    2. Aggregation
      1. Empty diamond
      2. weak "has-a" relationship (a pond has ducks in it, but they are not part of it, can exist without) 
    3. Composition
      1. Filled-in diamond
      2. strong "has-a" relationship (a book has words; cannot exist without them)
    4. Number of elements it can have (1, 1..n, 0..n) on each side of link
  3. Sequence Diagram (dynamic)
    1. Classes are shown as vertical lines
    2. Calls to methods are shown as solid arrows, and then return values as dashed arrows
    3. When execution of a method is in the stack it's a solid box
    4. Method called and value returned written above calls to methods and returned values, respectively

### DRY

* Don't Repeat Yourself

```java
public class Bird {

  // Lots of private methods here

  public void chirp() {
    openBeak();
    moveTongueDown();
    inhale();
    makeLoudNoise();
  }
  
  public void tweet() {
    openBeak();
    moveTongueDown();
    inhale();
    makeQuietNoise();
  }

}
```

* If you find yourself copy/pasting, BAD
* If you can refactor into methods, much better
* Why?  
  * Easier to understand
  * Less likely to make a mistake (esp. copy / paste error)
  * If you make change in one area, only have to change one place instead of all over

```java
public class Bird {

  private void prepareForNoise() {
    openBeak();
    moveTongueDown();
    inhale();
  }
    
   public void chirp() {
     prepareForNoise();
     makeLoudNoise();
   }

   public void tweet() {
     prepareForNoise();
     makeQuietNoise();
   }

}
```

* Also remember that you can use params to help DRY things up!

```java
// ...
  private void makeLoudNoise() {
     prepareSyrinx();
     vibrateSyrinx(100);
  }
  
  private void makeQuietNoise() {
    prepareSyrinx();
    vibrateSyrinx(20);
  }
```

* Why not this?

```java

   private static final int LOUD = 100;
   private static final int QUIET = 20;

  private void makeNoise(int level) {
    prepareSyrinx();
    vibrateSyrinx(level);
  }
```

* Also as part of DRY, think of one way to do things - use the same library, etc.

```java
  public int doubleMe(int i) {
    return 2 * i;
  }
  
  public int doubleAnInteger(int integerToDouble) {
    return integerToDouble * 2;
  }
```

### SOLID Principles

1. Single Responsibility Principle
  1. A class should have a single responsibility, do one thing and do it well
  2. In other words, high cohesion
  3. If you can't describe the class wtihout using "and", that's a code smell
2. Open Close Principle
  1. Classes should be open for extension, closed to modification
  2. This means that aside from bug fixes, make new subclasses, don't add to a class
  3. If classes keep getting bigger, that's a code smell from a 
3. Liskov Substitution Principle
  1. A class B which is a subclass of class A should implement any method in A and meet all invariants
  2. In other words, a subclass should be able to fill in for any of its superclasses
4. Interface Segregation Principle  
  1. Classes should not depend upon methods that they don't use
  2. In practice, this means lots of small interfaces / superclasses / abstract classes
5. Dependency Inversion Principle
  1. Depend upon abstractions, not concrete instances
  2. Don't depend upon specific items, but make interfaces / abstractions which can be filled in later
  
* Drawbacks to SOLID Principles
  * Often conflict with agile development
  * Should be taken as heuristics
  * Performance - massive structures of objects often a drag on speed / memory usage
  * Understandability can be compromised (see FizzBuzz enterprise edition)