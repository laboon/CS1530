## Final Study Guide

__Reminder: Final is Wednesday, 29 June!__

__The final is cumulative.  Everything we have discussed in class or in the readings is fair game.  Be sure to review all of the topics here and on the midterm study guide.__

1. Integration and the Software Pipeline
  * Phased vs incremental integration
  * Integration strategies:
    * Top-down
    * Bottom-up
    * Risk-oriented
    * Feature-oriented
  * Define smoke test
  * Continuous integration
  * Feature toggles

2. Quality Assurance
  * Internal vs external quality
  * Functional vs non-functional attributes (quality attributes)
  * White / grey / black-box testing
  * Code review vs code inspection
  * Unit / component / integration / regression / system / perfomance testing
  * TDD definitions - when is TDD not a good choice?
  * Boundary analysis
    * Explicit boundaries
    * Implicit boundaries
    * Compound boundaries
  * Base, edge, corner cases
  * Common errors:
    * Off-by-one errors
    * Incorrect logic
    * Security issues
    * Null pointer exceptions
    * Divide by zero
    * Ambiguous requirements

3.  Software Craftsmanship
  * Intellectual manageability of code
  * Being intellectually humble

4. Programming in a Multi-Threaded Environment
  * Understand what a thread is, how it differs from a process
  * Benefits of threading?
  * Problems with threading?
    * Race conditions
    * Livelock
    * Deadlock
    * Starvation
  * Understand what synchronized does and why you would use it
  * How to avoid threading problems

5. Software Maintenance and Refactoring
  * Two kinds of software evolution
    * Construction
    * Maintenance
    * What are similarities / differences?
  * Understand why to refactor code
  * Specific refactoring techniques:
    * Name/constant-ize magic numbers
    * Do not re-use variables
    * Don't query and modify in same method or same statement
    * Null objects
    * Class elimination
    * Decompose complex expressions
    * DRY up code

6. Dealing with Legacy Code
  * Definition and implications
  * Understand how to change
    * Pinning (aka characterization tests)
    * Inflection points
  * Sprout and wrapper methods/classes

7. Designing Secure Software
  * Why is writing secure software difficult?
  * Name the three elements of the InfoSec triad
  * Understand difference between vulnerability and exploit
  * Understand different kinds of vulnerabilities, esp.
    * Injection attacks
    * XSS (cross-site scripting)
    * Buffer overruns
    * Social engineering

8. Designing Performant Software
  * Is it better to be right or fast?
  * Performance threshold vs target
  * Know of several ways to improve code performance without code tuning
  * Jackson's Law of Code Tuning
  * Pareto Principle
  * Know the following code tuning techniques:
    * Unrolling loops
    * Jamming loops
    * Lookup tables
    * Lazy and eager evaluation
    * Short-circuiting

9. Trade-Offs in Software Engineering
  * Be able to make trade-offs using the "cost/benefit" method described in class
  * Be able to distinguish between NECESSARY and NICE-TO-HAVE features and quality attributes
  * Understand difference in trade-offs in internal quality vs external quality.  Which are preferable?  When?

9. Stakeholder Interaction
  * Understand what a stakeholder is
  * Know different stakeholder classes, their languages and what they care about
  * Understand managing expectations
  * Be able to make a red-yellow-green templated status report