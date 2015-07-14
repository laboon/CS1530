## Performance

* Remember, it's more important to make it _right_ than make it _fast_
* Sometimes, though, making it fast is making it right
  * e.g., performance requirements, KPIs, etc.
  * Although even then, ensure that it's a _real_ requirement

### Ways to improve code performance

1. Easiest way - upgrade hardware
2. Double-check requirements (target vs. threshold distinction)
2. Change program design
3. Language / Library choice
  * Compiled vs Interpreted language
  * Trade-offs in ease of development / readability / etc.
4. Code tuning
  * Modifying correct code so it runs more efficiently

```
Jackson's Laws of Code Tuning
1. Don't do it.
2. (For experts only) Don't do it yet.
```

* Remember the Pareto Principle!
  * Empirical study by Knuth: 96% of code execution time in 4% of code!
  * "You don't know jack until you've benched it." -Bob Hansen

* Compiler will optimize for you much of the time!
  * In C code, especially. gcc has all sorts of optimization flags
  * In Java, JVM actually does much of the optimization. 
    * There are JVM flags you can use, which are usually only helpful in special cases, but do help tune

* Common Sources of Inefficiency
  * Disk or Network I/O, in general
  * Paging to disk
  * System calls
  * Leaving debugging mode on, leaving debugging code around, extra println()s, etc.

* But how do you know where to fix?
  * You have to measure
  * More often than not, where the code ends up executing may surprise you (for non-trivial programs)
  * Using a profile
  * Example: VisualVM

* Figure out where issues are
  * Service-oriented
  * Efficiency-oriented
  * Use service-oriented issues to find problems, track down and fix with efficiency-oriented testing

* Code tuning techniques
  * General logic
  * Change algorithm
  * Short-circuiting
  * Ordering tests by frequency
  * Different data structures
  * Lookup tables
    * Doom "random number generator"
  * Lazy or eager evaluation
  * Loops - big place for efficiency gains
    * Unswitching loops
    * Jamming loops
    * Unrolling loops
  * Minimize work inside loop
  * Use sentinel values
  * Strength reduction
  * Use integers and not floating point values
  * Use as few array dimensions as possible
  * Caching
    * Dynamic programming
  * Initialize at compile time / hard code constants
  * Avoid system routine
  * Inline routines
  * Recode in lower-level language (e.g. inline assembly)  

* But remember to test if you actually made an improvement
  * Via benchmarking or profiler
  * Compilers are _quite_ good nowadays

