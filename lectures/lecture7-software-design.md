# Software Design

* Previously, we talked about the tactics of developing in a TDD manner
  * Red-green-refactor
  * Developing easily testable methods
  * Preparing for change

* This is going to be a mostly top-down discussion of software architectures

* No silver bullets, but there are some things that we have learned have worked.  

* As we go through, think about how to apply the lessons in Code Complete, especially:
  * Software design is a "wicked" process.  "Wicked": Sometimes the only way to know how to do it is to do it!  Example: Tacoma Narrows Bridge
  * Heuristics.  We have yet to come up with a one-size-fits-all approach
  * Sloppy - you will make mistakes.  Agile/Scrum takes this into account!
  * Trade-offs!  Everything is a trade-off, including your architectural pattern.

* Accidental and essential difficulties
  * Essential difficulties: inherent to the problem software is trying to solve
  * Accidental: Just happen to be part of the problem
  * Examples:
    * Essential difficulty: Ugh, this machine learning algorithm is hard to understand
    * Accidental difficulty: Ugh, why are we programming this ML algorithm in Assembly?

* Complexity is almost an essential difficulty in writing software, trick is to manage it
  * Minimize essential complexity (through abstraction, patterns, info hiding, encapsulation, etc)
  * Minimize accidental complexity

* One thing that architectural patterns need to do is break a system down into subsystems
  * Should be able to whiteboard these out, high level of abstraction
  * Software that is not easily whiteboardable is a code smell
    * Code smell - a hint that something might be wrong.  Does not mean that something is DEFINITELY wrong, but just a hint.
  * These subsystems should be cohesive:
    * Business rules
    * User Interface
    * Database Access
  * Just like objects!  Remember that classes should have very specific input/output, can have complex innards that are encapsulated / use information hiding
  * Again just like objects, there should be loose coupling / high cohesion!
  * Layers of abstraction all the way up!  Same basic concepts, just at a higher level.
  * Wheeler's Law: All problems in computer science can be solved by another level of abstraction.
    * Henney's Corollary "...except for the problem of too many layers of indirection."
    * Fun fact: David Wheeler was the first person in the world to get a PhD in computer science

* Listing of Design Heuristics
  * If possible, map from real world
    * Example: Super Mario Brothers video game
      * User Interface: controller input, screen output
      * World: contains one instance of Mario, instances of Question Mark block, Brick Block, Goombas, etc.
      * Data Storage: Stored level info, saved games, high scores, etc.
  * Be consistent when creating abstractions
  * Encapsulate Implementation Details
  * Information Hiding
  * Identify areas where change is likely
  * Loose coupling, high cohesion
  * Use standardized language
  * Use common design patterns

* Avoid leaky abstractions!
  * If you need to know about the innards of a class, this is a fail
  * If you need to know about the innards of a subsystem, this is a fail

## Common Architecture Patterns

* Software Architecture Patterns book (from O'Reilly) available online: http://www.oreilly.com/programming/free/files/software-architecture-patterns.pdf

* Layered Architecture
  * Think of a layer cake, or different geographical layers
  * Each layer is a deeper abstraction level
  * Separation of concerns
  * Think of your computer right now - layered abstraction maps very well to it
    * Application 
    * Operating System tools / libraries
    * Kernel
    * Processor / firmware / hardware / etc.
  * Each layer can only call down into deeper layer deeper, or other elements in its layer
    * This implies that you cannot call above your layer of abstraction - the kernel does not call code in Microsoft Word, for instance
  * Similarly, inside your program you can make layers
  * Very common layout:
    * Presentation Layer - Display data
    * Application Layer - Perform business logic on it and write to data layer
    * Data Layer - Get/save data
  * Or:
    * Presentation - How data is displayed
    * Business - Business logic itself
    * Persistence - When / how to store
    * Database - Actually store the data

* Variant: Model-View-Controller
  * Model: How the information is stored, business logic
  * View: How the user sees the data
  * Controller: How the model and view communicate
  * Model updates View, View uses Controller, which manipulates Model, loop forever

* N-Tier
  * Tiers are basically physical instantiations of layers
  * Run and separated on actual machines or hardware

* Client-Server
  * A special variant of n-tier, with two layers
    * Front-end: Usually just the visual display / presentation layer
    * Back-end: Everything else
  * This is where you hear about the divide between front-end and back-end developers

* N-Tier Example With Web
  * Front-end: the local web client (e.g. Internet Explorer, Chrome, Firefox)
  * Application Server: Ruby on Rails or other web server
  * Data Server: Database or other data store

* Blackboard
  * One piece of data
  * Lots of sub-processes working on it
  * Sub-processes do not communicate directly with each other, only with the data
  * Example: Visual processing

* Pipeline
  * Data moves forward through processes in a directed manner
  * Input > foo > bar > baz > quux > OUTPUT
  * Best example - Unix pipes / file redirects

* Event-driven Architecture
  * Flow of application driven by events
  * Usually a communications layer and multiple processes "listening" and "talking"
  * Example: fire alarm system, Java Swing framework

* Microkernel Architecture
  * Subsystem "plug in" to the main system
  * Main system is usually relatively small
  * Example: Eclipse

* Big Ball of Mud ( http://www.laputan.org/mud/ )
  * Most popular kind of architecture!
  * Usually starts out as another kind of architecture, slowly morphs
  * Add something here!  Ugly hacks!  Etc.
  * Lots of spaghetti code, leaky abstractions, held together with duct tape and gum

* How do we avoid the Big Ball of Mud?
  * Avoid integrating throwaway/prototype code
  * Rigid code reviews
  * Modularize ruthlessly

* Next time: class-level design patterns
