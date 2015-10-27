* What is integration?  Combining separate software components into a larger system
  * Could be classes -> program, programs -> application, servers -> n-tier system, whatever
  * Could take minutes, could take weeks
  * But always contains more potential than average for defects to crop up

* What is the problem?
  * Developers work on smaller parts of the project and understand that small part
  * Different assumptions can cause work to not interface with other teams' work
    * Mars Climate Orbiter - crashed because Lockheed Martin subsystem used American units, NASA subsystem (and rest of system) used metric
      * Note in this case, Software Interface Spec actually did define input/output to be metric
    * Gimli Glider - filled up fuel using old imperial units instead of metric

* Unknown issues - Stateful regex!

```javascript
pattern = new RegExp("foo","g");
pattern.test("foo bar")
=> true
pattern.test("foo bar")
=> false
```

* Wrong assumptions - "Ahh, I assume everybody will use well-known Java exceptions..."

* Other possible issues:
  * Subsystem doesn't build
  * Subsystem just doesn't function correctly
  * Interface not to spec, or problems in spec
  * Performance or other non-functional problems
    * A HUGE issue.  Often difficult to measure non-functional until late in the game.
  * Subsystem not reliable
  * One system ready, another not

* These are big issues in mixed hardware/software systems, especially if hardware can't be shipped until after software is written!

### Kinds of Integration

* Phased - original version
  * Design/code/test/debug each class/unit
  * Combine everything at once
  * System blows up.  Fix, fix, fix.
  * Release version __n__!

* Lots of drawbacks
  * If there is a defect, could be anywhere
  * Usually done at end of schedule - if any problems, may need to push back release
  * Time to panic - may take shortcuts to get out the door on time

* Incremental
  * Design/code/test/debug new class/unit
  * Add to system
  * Perhaps minor blow-ups.  Fix.
  * Now have version __n.0__, next time __n.1__, etc.

* Why is this better?
  * Errors easier to find (less code changed, smaller steps, etc.)
  * Integration is done throughout project (remember, things done often tend to be done right)
  * Failures found earlier
  * Monitoring progress is easier
  * Improved customer / developer morale (x / 10 features are complete!  huzzah!)

* Lots of strategies
  * Top-down: work on highest-level classes (e.g. highest layer in a layered architecture)
  * Bottom-up: work on lowest-level classes (e.g. bottom layer in a layered architecture)
  * Risk-oriented: work on the riskiest parts first
  * Feature-oriented: group by feature, not by class
  * T-shaped: Start top-down, then go all the way on one chunk first, then another, etc.  Can be similar to feature-oriented

* Daily build and smoke test?
  * Ensure once per day or so that system is working (compiles, tests pass, manual smoke test)
  * Will usually require a build group or person for non-trivial projects
  * Often a penalty for breaking the build (e.g. build chicken)
    * Side note: clever customs can help build team cohesion, but also may make it difficult to communicate outside team

* Continuous Integration
  * Pooh-poohed by Code Complete, but tools have improved!
  * Also companies mentioned: Amazon, Boeing, Expedia, Microsoft... notice anything?
  * Integrate each change with build within hours (original definition: at least daily)
  * At TTM, depending on QA, could be much less than an hour
  * Heavy reliance on automation

* Adding a feature to the system using CI
  * Get user story from backlog
  * Developer works on it (writes code, writes tests, smoke tests)
  * Push to github
    * Several things automatically happen
      * Hound: does automatic code review
      * Automated tests kick off
      * If flag set, will auto-assign code reviewers
  * If no hound comments and tests pass, code reviewers review code, set flag
  * QA person automatically assigned
  * QA does final check and merges if good

* One problem - long-running features or changes
  * Solution: feature toggles
  * Turn features off and on
  * Add complexity, but also allow for CI
  * Also allow for accidental release of new features if you forget to add some UI in a toggle!

```java
if (FeatureToggles.get("Survey") == true) {
    showSurvey();
} else {
    showDefaultMessage();
}
```

### Further Reading
Cataldo, M. and Herbsleb, J.  "Factors Leading to Integration Failures in Global Feature Oriented Development: An Empirical Analysis" (http://delivery.acm.org/10.1145/1990000/1985816/p161-cataldo.pdf?ip=150.212.123.236&id=1985816&acc=ACTIVE%20SERVICE&key=AA86BE8B6928DDC7%2E3F18A282B75518AA%2E4D4702B0C3E38B35%2E4D4702B0C3E38B35&CFID=520130042&CFTOKEN=54222915&__acm__=1434554321_f2bbd30d4f0234db0ecf0208becf00220)

Code Complete chapter 29


Muller, G. "Why is Systems Integration understood so poorly? Reflections on 3 decades of unforeseen failures" (http://www.gaudisite.nl/SystemsIntegrationReflectionKSEESlides.pdf)

Netflix Tech Blog, "Preparing Netflix API for Deployment" (http://techblog.netflix.com/2013/11/preparing-netflix-api-for-deployment.html)