# CS 1530 - Software Engineering
Summer Semester 2015

## DUE DATE: 8 JUL 2015

## Deliverable 3

For the third sprint, each group will continue implementing user stories.  You will also turn in several other reports - see the Format section, below.

The major change in this sprint is the addition of code reviews.  Before it is merged to master, all code will be reviewed by somebody who did not write it.  The easiest way to do this is to submit it as a pull request, which we will go over in class.  The method used for allocating code reviews is up to you, but it's usually easiest to rotate the responsibility (person 1 checks the first PR, person 2 the second, etc.)  You may also decide to have your QA person check all the code.

Up to one fifth (20%) of the grade will consist of marks from your fellow team members.  If you think that people in your group have done basically the same amount and quality of work, you can ignore this, and everybody in the group will get the same grade.  If you feel that there has been a disparity, you may email me (privately) with a listing of every member in the group (including yourself) about the amount of work done, in your opinion:

0. The person did no work at all, did not respond to emails, etc.
1. The person did minimal work, but did not complete it or it was unsatisfactory
2. The person did less work than other members
3. The person did about the same amount of work as other members
4. The person did much more or higher quality work than other members

If people in a group report disparities, I will assume that the git commit history holds the truth and will investigate.  At this point, I will grade people separately based on what I see in the git commit history.  Remember that I will be able to see who committed what to the repository so please commit under your own username!  For this reason, you should probably commit the final reports as well (although I will still expect a printed out copy).

## Format

For the first sprint, you will turn in:

1. A cover page, in the format described below
1. An approximately one or two page description of what was accomplished this sprint.  This should include __at least__ the following details, but you may provide more:
  * What disagreements arose, and how they were solved (if any)
  * How did you integrate different people's work?
  * Changes in process since last sprint
  * Experience in code reviewing 
  * Interactions with customer
  * Challenges writing the code or tests
2. User stories completed this sprint, and a link to the code on GitHub
3. Details on why you decided on those user stories
3. A list of any defects found by testing, and how they were discovered and fixed (or if not fixed, why you decided not to prioritize them).  This can include defects found by unit testing or system testing by QA (or other methods, such as issues found by the customer).  If no defects were found, then please write a paper on how you have developed a way to develop software without making any mistakes, because I would be happy to read it!

Each of these sections shall be CLEARLY MARKED (i.e. they should each have titles and start on their own page).

Format for cover page:
* The name of the project
* The names of the people in the group, and their git usernames
* The date that it is due (8 JULY 2015)
* The title "CS 1530 - SPRINT 3 DELIVERABLE"

## Grading

* Listing of Completed User Stories and Why Chosen: 10% of grade
* Description of Sprint: 10% of grade
* Listing of Defects (can be defects found in code review, as well): 10% of grade
* Code, Tests, and Code Reviews: 50% of grade
* Group Rating*: 20% of grade

Yes, grammar and spelling count.  Points will be deducted for more than one grammatical or spelling error per section.

Code should be well-tested; you don't need to do "official" TDD (although I recommend you do so), but there should be good code coverage of common use cases for many, if not most, methods.  You should use design patterns when appropriate.

Defects should include at least the following information:

1. Reproduction Steps (or reference unit test that caught failure)
2. Expected Behavior
3. Observed Behavior

If nobody from the group submits a group rating, then this segment will not be used, and all other sections will be adjusted (the first three being worth 12.5% of grade instead of 10%, and code, tests and code reviews being worth 62.5%).

## Other

Please feel free to email me at bill@billlaboon.com or come to office hours to discuss any problems you have. 
 
