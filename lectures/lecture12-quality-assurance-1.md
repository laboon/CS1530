## Software Quality and Quality Assurnce

* What do we mean by quality software?
  * External quality
    * Functional attributes - software is free from faults in design, implementation, returns correct results
      * Correct: Does what the user wants and expects (checking for this is validation)
      * Accurate: How well does it do that job? (checking for this is verification)
    * Non-functional attributes (quality attributes) - Software is usable, efficient, reliable, scalable, adaptable, etc.
  * Internal quality
    * Things programmers see - is program maintainable?  flexible?  portable?  readable?  etc.
  * Sometimes these things overlap
  * But always, always, always tradeoffs
  * Keep this in mind: software engineering is the study of tradeoffs

* There is a common misconception that software quality is the same as software testing.
  * Not the truth - testing is simply a part of ensuring quality

* Explicit quality goals and activity
  * Let developers know that speed is not the most essential item
  * SR-71 Blackbird: speed above all else (record for fastest airplane) 
    * None lost to enemy action - if a missile fired, SOP was to just accelerate and outrun it
    * Very expensive, custom-made parts (increasingly difficult to find / manufacture)
    * Needed a "start cart" - could not start engines on its own
    * Pilots needed to wear a pressurized suit
    * Very hard to maintain: tires were filled with nitrogen, airframe was over 500 degrees hot after it landed
    * No data link
    * Leaked fuel on the runway - ruptures sealed once it reached altitude
    * See any parallels with software development?
  * Developers will work to objectives
  * Study done, told developers to work for a specific goal
    * Minimum memory use, most readable output, most readable code, least amount of code, minimum programming time
    * In 4 / 5 cases, programmers were #1 in the category that they optimized (last case, they were #2).  In all of the cases, at least one of the other categories, they were the worst.
    * Trade-offs!

* Pair programming 
  * You've already done this!
  * Person "looking over your shoulder", can find errors / edge cases / better way to do things
  * Is a bit slower in short run, most studies show better when viewed holistically

* Code reviews
  * Other person takes a look at code
  * What to look for?
    * Better ways to do things
    * Magic numbers, hard-to-read code
    * Performance improvements
    * Better design
    * Logic errors
    * Edge cases that are not handled appropriately
  * Tend to find fewer errors than pair programming!  Faster in short run, though.

* Code inspections
  * More formal, specific roles
    * Moderator, author, reviewers, scribe
    * Usually no management
  * Very effective, but very expensive
  * Multi-step
    * Planning - author gives code to moderator, who puts together a meeting
    * Overview - author describes environment, provides initial information, background, etc. (sometimes unnecessary)
    * Preparation - Each reviewer reviews code for a while, perhaps from different perspectives (security, performance, readability, etc.)
    * Inspection meeting - Go through (class by class, e.g.) code - do not discuss solutions, only problems
    * Inspection Report - Moderator produces report listing all defects found
    * Rework - Author fixes defects found
    * Follow-up - This may be as simple as moderator reviewing it, to reviewers re-reviewing it, to a full-on meeting
  * Finds more errors than any other collaborative system talked about today, but at big cost

* Code walkthroughs
  * A combination of inspection and review
  * Reviewers read code, author walks through it
  * Emphasis on error detection, not correction
  * Again, keep management out

* Dog and Pony Show
  * Show off the software to a customer
  * Ensures that software is at least somewhat working
  * Make sure you are on right path with customer
  * Downside: focus is on external quality, not internal quality

* Remember to criticize the CODE, not the PERSON!

* Multi-modal, multi-person inspection
  * People find different defects
  * Strategies find different defects
  * Best way to find more - multi-person, multi-modal

* Finding and Fixing Defects
  * Longer it takes to find them, more black-box they get, the harder it is to fix them  

* Collaborative Construction
  * Pair programming, formal inspections, informal reviews, etc.
  * Developers share responsibility
  * "Criticize the code, not the person"

* Code reviews and inspection are a huge win - defects are found and also easily fixable

* Provides mentoring automatically!
  * As long as pairs are mixed

* Collaborative development tends to find more defects than testing

* The General Principle of Software Quality
  * In the long run, writing quality software is free due to the time saved in development
  * In the short run, seems more expensive
  * Numerous studies have shown that time/resources saved by producing quality software more than make up for extra time (for larger products)
    * Why?  Better code, fewer defects, defects fixed sooner
  * Read some Paul Graham - sometimes better to put out something and iterate
    * When your "customer" is lots of people - e.g. Facebook, Dropbox, etc.
    * "If you're not embarrassed by your first version, you waited too long to ship"
    * Side note: Graham wrote some very interesting, thought-provoking articles on software engineering earlier in his career (now it's mostly marketing).  See "Why Arc Isn't Especially Object-Oriented" ( http://www.paulgraham.com/noop.html ), "Java's Cover" ( http://www.paulgraham.com/javacover.html ), and "Beating the Averages" ( http://www.paulgraham.com/avg.html ).  All are over a decade old, but very relevant.
    
* When to do quality assurance?
  * ASAP
  * Earlier that a defect is caught, earlier and cheaper it can be fixed  