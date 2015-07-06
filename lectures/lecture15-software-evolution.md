## Software Maintenance, Evolution, and Refactoring

### In The Beginning Was The End

* You want your programs to evolve, not devolve
* Leave codebase better than you found it!
* Codebase is __constantly__ evolving
  * Requirements tend to change by about 1-4% per month
  * People modify system as they understand the software/problem
  * Modern software development methodologies (e.g., Agile/Scrum!) assume change is taking place
* Ask - is my change making the software evolve or devolve?
  * Devolve - Harder to change. Harder to understand. Less test coverage. More convoluted. More defects.
  * Evolve - Future changes easier. Easier to understand. More test coverage. Less convoluted. Fewer defects.
  * If refactoring is "baked in" (e.g. the red-green-refactor loop), then every change is a chance to make software better
    * Older paradigms resisted code change, meant every (inevitable) change was more likely to make software worse

* Traditionally, two kinds of software evolution
  * Construction
    * Done during initial creation of software
    * Often by same developers working on creation
    * Penalty for making mistakes low
  * Maintenance
    * Done after initial version released
    * Often done by people unfamiliar with initial design
    * Penalty for making mistakes higher

* Key to ensuring proper evolution: understanding difference between fixing defects, adding features, and refactoring

* Fixing defects: Program modifications are made to change a small piece of functionality so that it produces valid results

* Feature addition: Usually larger than defect fixes, adds additional functionality to a piece of software.

* Refactoring: a change made to make the software easier to understand, easier to modify, etc. without changing its observable behavior
  * Why refactoring? Original name for deconstructing a system into small pieces was "factoring", so this would be "factoring again"

* Look at some code... why should you refactor it?
  * Code is duplicated - DRY principle
  * Long routines / methods
  * A loop is too long or too deeply nested
  * Low cohesion
  * Inconsistent abstraction
  * Large numbers of parameters on methods
  * Tight coupling - modification of one class means modification of others
  * Poor organization - possibility of modifying one thing, forgetting to modify others
  * "Tramp data"
  * Class or method no longer used
  * Overloading of primitives
  * Bad hierarchy - does a subclass really belong to its superclass?
  * Lots of public data members, if class is not just a "struct++"
  * Comments are explaining difficult code
    * "Don't document bad code - rewrite it"
  * Reliance on global variables (this is almost ALWAYS bad)
  * Lots of setup / teardown code
  * Code that "I might need someday"
    * YAGNI!
    * If you are using version control, can always go back and get it later

* Refactoring can be done at different levels of abstraction
  * Read "Refactoring" by Fowler if you want to go into even more depth

* Statement- and method-level
  * Magic numbers should be named
  * Rename variables
  * Expression inlined, or made into an intermediate variable
  * Stop re-using variables
  * Use a local variable instead of a parameter
  * Don't query and modify on the same statement or in the same method
  * Combine routines by parameterizing, or separate routines to have no params
  * Pass a whole object instead of specific fields, or vice-versa
  * Encapsulate at lowest level possible
    * Prefer HashMap over Map over Object
  * Decompose complex expressions
  * Complex Boolean expression? Why not a separate method?

* Class-level
  * Change method or attribute placement
    * Does method belong in super or subclass?
    * Does attribute belong in super or subclass?
    * Does method/attribute even belong in this class?
  * Extract specialized code into a subclass
  * Combine similar code into a superclass
  * Convert class into multiple classes
  * Remove or add "middleman classes"
  * Eliminate a class
  * Do you even need object hierarchies?
  * Check that methods not used outside of class are private 
  * Use null objects

* System-level
  * Create a definitive reference source for external data ("ground truth")
  * How should you indicate errors?  Exceptions?  Error codes?  Other?
  * Use design patterns when necessary


* Pain-free refactoring
  * Don't throw away the code you start with
    * Yay, git!  Yay, branches!
  * Small refactorings
  * Refactor ONE THING AT A TIME
    * You can keep a list of other things you see
    * I would often keep track in GitHub comments
  * Frequent checkpoints - run tests
  * Tests, tests, tests
    * Run old tests
    * Create pinning tests
  * Compiler warnings are your friend
  * Code review!
    * One org: reviews for one-line changes meant a drop in error rate from 55% to 2%
  * Adjust approach based on riskiness
  * Remember that refactoring is NOT changing functionality
    * Try to differentiate between the two, keep separate commits or PRs

* Strategies for refactoring
  * Red-green-refactor puts in time
  * If using another methodology, could look at refactoring:
    * Before/after adding a class
    * Before/after adding a method
    * When fixing a defect
  * Target error-prone or highly complex methods
  * Clean/ugly code boundaries - move stuff to clean code
    * Real world is a mess -> clean up, clean up -> lovely Platonic world
    * Better than putting in lots of exceptions/checks in the middle of code
    * Deal with it at the edges
    * Example: CDRIS getting data from lots of systems