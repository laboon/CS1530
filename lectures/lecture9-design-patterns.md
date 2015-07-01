## Object-Oriented Design Patterns

* The Gang of Four Book, "Design Patterns: Elements of Reusable Object-Oriented Software"

* Different patterns at the above-statement-level, below-system-level

* Code Complete mentions many of these, but does not describe or implement them, just says "use patterns"

* Patterns will be different in different languages (e.g. Strategy is kind of ridiculous in a language where functions are first-class objects)

* NOTE THAT NONE OF THESE EXAMPLES HAS BEEN CHECKED FOR THREAD SAFETY, AND MOST ARE DEFINITELY NOT THREAD-SAFE.  THEY ARE EXAMPLES ONLY!!!

1. Utility Pattern
  * Perhaps the simplest pattern - does not allow instantiation
  * Useful for utility methods, e.g. tools
  * All static methods
  * Has no state!  Everything must be passed in as a param to a particular method

```java
public static class Math {

   public static int square(int n) {
       return n * n;
   }

   public static int cube(int n) {
      return n * n * n;
   }


}
```

1. Singleton
  * Used when you want to ensure there is only one instance of a given class
  * Can use lazy evalutation - not generated until needed
  * Why use this instead of Utility?  Can implement interfaces!
  * Use for: database or other connections, any time you want to ensure a single instantiation

```java
public class ProfessorLaboon {
   private static ProfessorLaboon _instance = null;
   protected ProfessorLaboon() {  }
   public static ProfessorLaboon getInstance() {
      if(_instance == null) {
         _instance = new ProfessorLaboon();
      }
      return _instance;
   }
}
```
  * Drawbacks: 
    * Can often just use static methods
    * Worries about thread safety
    * Makes unit testing more difficult, since global state introduced

1. Factory
  * Different versions of a method return different classes

```java
public class Bird {

    public void doBirdStuff() {
        BirdNoise bn = getBirdNoise();
        bn.makeNoise();
    }

    protected BirdNoise getBirdNoise() {
        return new GenericTweet();
    }

}

public class Duck extends Bird {

    @Override
    protected BirdNoise getBirdNoise() {
        return new Quack();
    }


}

```

1. Decorator
  * Dynamically decorate an object from its base
  * Generates a new decorated object

```java

public interface CoyoteInterface {

    public void chase(RoadRunner r);

}

public class Coyote implements CoyoteInterface {

    public void chase(RoadRunner r) { ... }

}

abstract class CoyoteDecorator implements Coyote {

   public void chase(RoadRunner r) { ... }

}

public class CoyoteRocketDecorator extends {

    private _decoratedCoyote = null;

    public CoyoteRocketDecorator(Coyote c) { 
        _decoratedCoyote = c;
    }

    public void chase(RoadRunner r) {
        super(r);
        chaseOnRocket(r);
    }

    private void chaseOnRocket(RoadRunner r) { ... }

}

public class CoyoteRollerSkatesDecorator extends {

    private _decoratedCoyote = null;

    public CoyoteRocketDecorator(Coyote c) { 
        _decoratedCoyote = c;
    }

    public void chase(RoadRunner r) {
        super(r);
        chaseOnRollerSkates(r);
    }

    private void chaseOnRollerSkates(RoadRunner r) { ... }

}



```

1. Pool
  * Store a bunch of objects around, can re-use
  * Can create ahead of time (opposite of lazy, super-eager)
  * Thread or Object
  * Should use a library, e.g. GenericObjectPool from Apache

```java
public class RolexPool {

    private ArrayList _rolexes = new ArrayList<Rolex>();

    public Rolex getRolex() {
        if (_rolexes.isEmpty()) {
            // Generate some more Rolexes   
        } 
        // Get and return the first Rolex
    }

    public void returnRolex(Rolex r) {
       _rolexes.add(r);
    }

}
```

1. Iterator
  * Iterate over object collection
  * Java has the `Iterator` interface

```java
public class BirdIterator {

    Bird[] _birdsArray = null;

    int _nextLoc = 0;

    public BirdIterator(Collection birds) {
        _birdsCollection = birds.toArray();
    }

    public boolean hasNext() {
        return ( _nextLoc < _birdsArray.length));
    }

    public Bird next() {
        Bird birdToReturn = _birdsArray[_nextLoc];
        _nextLoc++;
        return birdToReturn;
    }

}
```
  
1. Strategy
  * Algorithm to be used will vary, can be passed in
  * Useful for when you have the same concept, but need to use different algorithms to implement it
```java
public interface Sorter {
   public int[] sort(int[] intsToSort);
}

public class BubbleSortSorter Sorter {
    public int[] sort(int[] intsToSort) { 
        // does bubble sort
    }
}

public class MergeSortSorter implements Sorter 
    public int[] sort(int[] intsToSort) { 
        // does merge sort
    }
}

public class Database {

    private Sorter _sorter = null;

    private int[] _storedInts = null;

    public Database(Sorter s, int[] someInts) {
        _sorter = s;
        _storedInts = someInts;
    }

    public int[] sortIntegersInDatabase() {
       _sorter.sort(_storedInts);
    }

}

```


1. Null Object
  * Instead of returning a null pointer reference, return an object with methods that don't do anything, or that return default values
  * Avoids NullPointerExceptions

```java
public interface Bird {
    public void chirp();
}

public class Turkey implements Bird {

    public void chirp() {
        System.out.println("Gobble gobble!");
    }

}

public class NullBird implements Bird {

    public void chirp() {

    }

}

// Get the bird in the cage - may or may not exist
Bird b = cage.getBird();
// Old way
// if (b == null) {
//     // do nothing
// } else {
//    b.chirp();
// }

// With Null Object pattern
// No need to null check because methods just won't do anything
b.chirp();

```

1. Flyweight
  * Bulk of object lies elsewhere
  * Instantiating it only creates items specific to that object
  * Example - String interning

