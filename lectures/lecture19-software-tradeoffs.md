## Trade-Offs in Software Engineering

* Remember the iron triangle
  * Scope
  * Resources
  * Time

* You can optimize according to time or resources
  * More people up front, trailing off
  * Remember your Brooks "adding more people to a late s/w project makes it later"

* However, oftentimes you have hard deadlines, or limited funds.
  * Thus need to compromise on scope.. but how?
  * Two different aspects
    * Quality Attributes (e.g., security, usability, performance)
    * Functional attributes (features)

* Determine - what is NECESSARY and what is a NICE-TO-HAVE
  * If a feature will get you 10 additional users, is it worth delaying delivery or cutting other features?  What about 100?  A million?  A billion?
  * Is internal quality better than external quality?
    * What if we need to upgrade Super Mario Bros?!?!
    * Does portability or maintainability help us here?
  * On the other hand.. would better internal quality have helped OpenSSL or GCC?
  * Internal quality often leads to better external quality, but NOT ALWAYS
  * Sometimes better to err to one side, sometimes the other.

* Make a list, check it twice, find out who's naughty XOR nice
  * List and quantify benefits / drawbacks
  * Come up with broad estimates of what's necessary
  * Work with PMs and other stakeholders to determine relative importance
  * In performance testing, there is the concept of threshold and target
    * What is your threshold of features?  What is your target?

* Example: The landing software for Apollo 11's LEM

* Example: Adding metrics to an online ed-tech program written in Ruby on Rails

* Example: Your group!
  * What kinds of 

* Further reading: "Software Quality Attributes and Trade-Offs" by Berender et al. https://www.uio.no/studier/emner/matnat/ifi/INF5180/v10/undervisningsmateriale/reading-materials/p10/Software_quality_attributes.pdf