## Legacy Code

* What is Legacy Code?
  * No official definition, but code that is already in use.
  * Kind of like a heap of sand - one grain is not a heap, is two?  three?  four? etc.
  * Implications:
    * User interfaces are unfriendly and error prone
    * Little to no documentation
    * Written without benefit of modern software practices
    * Written in rarely-used or obsolete language
    * Programs not organized and difficult to understand
    * Lots of inefficiencies, inconsistencies, redundancies, etc.
    * Expensive and difficult to modify
  * Defined by Michael Feathers as "code without tests"
  * Usually a pejorative term

* It's hard, it's thankless, it's not rewarding.
  * Nobody made a movie about someone spending five days trying to get the sales tax changes working on 45-year-old point of sales software.

* Why do it?
  * Changes necessary (e.g. sales tax changes) 
  * Add functionality
  * Fix defect
  * What is missing from this list?
    * Code is ugly
    * Code written in old language
    * If it ain't broke, don't fix it!
    * Avoid pre-emptive work on legacy code!

* Remember that any approach works with small programs!  Maybe the best case is a rewrite.

* For larger programs, not so much.  The reason that method is 500 lines long is that it probably fixed lots of edge cases.

* Ask three questions:
  * What exactly needs to be changed?
  * How do you check if they are correct?
  * How do you check that there are no regression failures from this change?

* Answer - use pinning tests
  * Pinning tests (also called "characterization tests" or "test covring") check the EXISTING behavior of a program
  * Not expected behavior, existing.  Very different!
  * Adds an invariant to the system (should be the same before/after)
  * Why would you do this?
    * Users may depend on these "glitches"
    * Understand what you're changing, even if it's a fix

* General strategy
  * Get to the point where you can make small changes - one bit at a time
  * Add pinning tests as you go
  * Soon you find yourself with a little, but ever-growing, test suite
  * Add traditional unit tests to it

1. Identify change points
2. Find an inflection point
3. Cover the inflection point with pinning tests
  1. Break external dependencies to it
  2. Break internal dependencies to it
  3. Write tests
4. Make Changes
5. Refactor Code

* Inflection point - a "chokepoint" in the system where changes can be made without breaking other pieces of the system

* External dependencies - talking to other objects

```java
class Bird {
  private _nest = new Nest();

  public void goHome() {
    flyTo(_nest);
  }
}
```

* Ugh ugh ugh!  Let's do some __dependency injection__:

```java
class Bird {
  public void goHome(Nest n) {
    flyTo(n);
  }
}
```

or

```java
class Bird {

  private _nest = null;

  public Bird(Nest nest) {
    _nest = nest;
  }

  public void goHome() {
    flyTo(_nest);
  }
}
```

* Break internal dependencies
  * Make very minor changes at this point!
  * May involve subclassing

* Refactor
  * Start making the code better
  * If you had to make changes, likely that other changes may need to be made, too


* Particular strategies
  * Sprout methods/classes

```java
public class OldStuff {

  public int addUpNums() {
    int toReturn = 0;
    for (int j=0; j < 10; j++) {
      toReturn += j;
    }
  }

}
```

How about adding only primes?

```java
public class OldStuff {

  public int addUpNums() {
    int toReturn = 0;
    for (int j=0; j < 10; j++) {
      if (// complicated code for figuring out if prime) {
        toReturn += j;
      }
    }
  }

}
```

BETTER

```java
public class OldStuff {

  // Easily testable
  public int getNumIfPrime(int num) {
    if (// complicated code for figuring out if prime) {
      return num;
    } else {
      return 0;
  }

  public int addUpNums() {
    int toReturn = 0;
    for (int j=0; j < 10; j++) {
      toReturn += getNumIfPrime(j);
    }
  }

}
```



  * Wrap methods/classes

```java
  public class OldStuff {

    public void doBoringUntestedStuff { ... }
    
    }
 
  }
```

```java
  public class OldStuff {

    private void doBoringUntestedStuff { ... }
    
    }

    public void doNewStuff() {
      // Fix preconditions
      doBoringUntestedStuff();
      // Fix postconditions
    }
 
  }
```


  * Identifying seams - places where you can make changes without modifying code
  * Or inflection points - places where code changes are localized, not going to cause problems elsewhere
  * Move TUFs (test-unfriendly features) out of TUCs (test-unfriendly constructs)
    * What are TUFs? Things that are hard to test
      * Database connections, file I/O, network interfaces, etc.
    * What are TUCs?  Areas it's hard to test things in
      * Constructors, destructors, final methods, static methods, private methods..

* Further reading: 
  * Essay, "Working Effectively with Legacy Code" by Michael Feathers. http://www.objectmentor.com/resources/articles/WorkingEffectivelyWithLegacyCode.pdf
  * He also wrote a book of the same name, which goes into more detail
  * Testable Java, http://www.objectmentor.com/resources/articles/TestableJava.pdf

