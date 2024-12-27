# Test-Driven Development by Example Notes

## Preface

- **TDD Goal:** Make clean code that works.
- The two rules of TDD are:
  - Write new code only if an automated test has failed
  - Eliminate duplication
- **Red - Green - Refactor:** This is the cycle followed in TDD:
  - **Red:** Write a test that doesn't work (not working includes not compiling)
  - **Green:** Make the test work (without worrying about code cleanliness)
  - **Refactor:** Eliminate duplication/mess created in the green stage
- **Motivation for TDD:**
  - It allows us to be confident in our programming. We can make big changes because we are confident the code still works afterwards (as passing tests provide this proof).
  - Reduces defect density
- **Note on the limit of TDD:**
  - TDD isn't the only way of programming, and doesn't work on all problems.
  - TDD can fall short when dealing with issues like security and concurrency.

## Part I: The Money Example

- The flow of TDD:
  - Quickly add a test (which only has to cover a small increment of functionality)
  - Run all tests and see the new one fail
  - Make a little change
  - Run all tests and see them all succeed
  - Refactor to remove duplication

### Chapter 1: Multi-Currency Money

- In TDD you always start with tests.
- When you want to add a new feature, split it  into a to-do list of tests. Then focus on each test in turn (following the red-green-refactor steps to cross each test off). Add new tests when you think of them to the list.
- When you write a test you are testing the API of some peice of code. Write the test imagining the perfect API of how you want the feature implemented. 
- By creating a test, you create a dependency between the test and the code. By reducing duplication as much as possible, you can help eliminate dependencies as much as possible.
- In the refactor step, you can take many small steps of refactoring (each time ensuring the tests are still green).

### Chapter 2: Degenerate Objects

-  TDD cycle:
  - **Write a test:** Write a "story" of the interface you wish you had, and the outputs of that interface
  - **Make it run:** Quickly get the bar to go green. Speed dominates everything else in this phase.
  - **Make it right:** Remove all duplication you have introduced/all code mess. This includes duplication between test and code.
- As you refactor the code, you may realise that the interface you defined in the first step, isn't actually the best way to implement the required behaviour. As part of refactoring you can change the test to fit with your new understanding of how the interface should work.
- **How to approach TDD - 3 stratergies:**
  - **Fake it:** To get to green, return a constant. Then when refactoring gradually remove constants till you have real code. (With faking values, you create data duplication. By removing this duplication you'll arrive at a proper implementation.)
  - **Use obvious implementation:** If there is an obvious solution, you can just implement this.
  - **Triangulation:** If you are struggling to see how to remove duplication, by adding more test cases it can help you generalise a problem.

### Chapter 3: Equality for All

- As you implement the code, new implied operations/functionality will be revealed. You can add those to the to-do list of tests.

### Chapter 4: Privacy

- Reducing coupling between tests and code is very useful. The less coupled the tests and code, the more you can refactor without breaking tests.

### Chapter 5: Franc-ly Speaking

- When implementing a new feature, you can start by making smaller tests that represent progress. These tests can help guide your development.

### Chapter 6: Equality for All, Redux

- When you are refactoring, you will often be dealing with code that doesn't have enough tests. You should write those tests retroactively before starting to refactor (to ensure that in the refactoring you don't break something).

### Chapter 8: Makin' Objects

- TDD works through many small steps. The smaller the step the more confident we can be (as it lets us get back to a state where all tests pass quicker).

### Chapter 9: Times We're Livin' In

- When working you may have a change to improve the code not needed to make the test pass. While strictly you shouldn't interrupt what you are doing, small interruptions can be permissible (although never interrupt an interruption).
- The more confident you are, the bigger the steps you can take (the "higher gear" you can be in). However, the less confident you are, the smaller the steps you should take. As you work, you will constantly shift the "gear" you are in to match your confidence.

### Chapter 10: Interesting Times

- With tests, instead of reasoning about whether something will work, you can emperically find the answer by running the tests.
- Try not to add new tests when a current test is failing. If you need to, then it is best to rollback changes to a "green" state and then add the new test.

### Chapter 11: The Root of All Evil

- As you are developing you will create tests along the way. However, these tests created to help you with the "in-between steps" may become useless as more tests are added. You should delete these "development" tests when they stop being useful.

### Chapter 17: Money Retrospective

- There are generally about the same number of lines of test code as functional code.
- TDD cycle:
  - Add a little test
  - Run all tests and fail
  - Make a change
  - Run the tests and succeed
  - Refactor to remove duplication
- While tests from TDD are useful they don't replace other types of testing like:
  - Performance testing
  - Stress testing
  - Usability testing
- **Measures of test quality:**
  - **Statement coverage:** Should be close to 100% if TDD being followed religiously.
  - **Defect insertion:** To test the quality of the tests, you can have a program automatically insert errors and see if the tests still pass. (This is also known as mutation testing.)
- You can improve test coverage by writing more tests. However you can also improve test coverage by simplifying the logic (through refactoring). As the code shrinks, the same tests will cover a greater portion of the code.
- **Key takeaways:**
  - Three approaches to making a test work cleanly:
    - Fake it
    - Triangulation
    - Obvious Implementation
  - Removing duplication between tests and code as a way to drive design
  - The ability to control the gap between tests to increase confidence in tricky problems, or move quickly when things are simple.

## Part II: The xUnit Example

### Chapter 18: First Steps to xUnit

- Refactoring pattern: Hardwire your code to work for one instance and then generalise it to work with all instances by replacing constants with variables.
  - This is an advantage of TDD, you can start by implementing concrete examples you know work, and then generalising from there (instead of having to jump directly to the generalised example).
- Don't be afraid to work in tiny steps (only changing a handful of lines at a time).