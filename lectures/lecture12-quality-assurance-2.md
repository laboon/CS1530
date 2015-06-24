## Software Testing

* All kinds of testing
  * Unit testing - JUnit, etc.  Work on smallest units of code.
  * Component testing - Execution of a class or package, tested in isolation.
  * Integration testing - Checking that systems, classes, etc. work together.
  * Regression testing - Ensuring that tests which previously passed still pass; that is, that the work you did did not introduce any new defects.
  * Systems Testing - Testing the final system as a whole.
  * Performance Testing - testing resource usage or speed of system
  * Security Testing - Ensuring adversaries cannot access your system
    * The InfoSec (CIA) triad
  * Lots of other kinds of testing 

* Black-box testing: testing as a user does, no knowledge of the codebase / interior of the system.
  * Benefits: See from POV of user of system, focus on what it should do and not how it does it
  * Drawbacks: Less knowledge of system, less knowledge of where it breaks down
  * Story: What happens in Java when you try to divide by zero?  What happens in JavaScript?

* White-box testing: testing as a developer, checking the inner workings of the system.
  * Benefits: Can check lots of edge cases, very low-level, very specific
  * Very low-level, not looking at system like a user
  * Story: kNN algorithm, using default sort

* Grey-box testing: a mix - look at code, then do black-box testing
  * Some of the pluses and minuses of each

* Things To Keep In Mind When Designing A Testing Strategy
  * Testing should be at least somewhat independent (remember pinata gif).  An indepedent perspective will find more errors.  
    * This does not mean that developers should not test!  Quality is everyone's responsibility.
  * Testing does not prove absence of defects!  Ever!  There is always the possibility of failures that you did not think of (e.g., threading and concurrency issues, edge cases, meteor strike, etc.)
  * Exhaustive testing is impossible.
  * Testing helps you to see software quality; it does not improve it on its own.  However, it is an important way to ensure that you are developing quality softare.

* Testing first - TDD
  * When doesn't TDD work well?  When you're not sure of the expected behavior
    * Examples: front-end dev, graphics, first-time algorithms
    * Often can break down into smaller pieces
    * But sometimes you just need to try it, figure it out, then write tests later

* What to test?

* Equivalence class partitioning

* Boundary analysis
  * Explicit boundaries
  * Implicit boundaries
  * Compound boundaries

* Good data, bad data
  * Base cases
  * Edge cases
  * Corner cases

* Kinds of Errors
  * Off-by-one errors: why boundary values are so important
  * Incorrect logic
  * Not handling invalid data correctly
  * Does not integrate correctly with other parts of the system
  * Performance issues
  * Security issues
  * Null pointer exceptions
  * Divide by zero errors
  * Ambiguous or incorrectly-interpreted requirements
  * Definitional issues

* Things to remember when testing
  * The scope of most errors is limited
  * Errors aren't always programming-related!  Often relate to communications or missing domain knowledge
  * Problem is usually the programmer.  Sometimes it's the libraries.  Not often the compiler, system software, hardware, etc.  
  * Automation is going to save you so, so much time in the long run
  * ... but automation only checks what it is looking for!
    * Usually a good idea to have a manual smoke test before release
    * Story: background color change
    * Error rate in manual testing is comparable to bug rate in the code being tested
    * Also a mind-numbing job.
  
* Pareto Principle - 80% of problems found in 20% of classes

* Testing focuses on finding defects, not fixing them, or even determining the general area where they lay
  * Debugging != testing

* Generating test data
  * For simple unit tests, can manually set up
  * Property-based testing: automatically generate data, check for properties
  * When dealing with generated test data, you have two (sometimes conflicting) goals:
    * Check that ordinary base cases (and most common use cases) work well
    * Check for edge cases and unusual combinations 
    * Best thing is real data (anonymized if necessary)

* Testing strategy
  * How much testing is necessary?
  * How much time should be focused on improving it?
    * CMMI - remember the final step is optimizing - you need to do lots of work to get to that point
  * What kinds of testing should you do?