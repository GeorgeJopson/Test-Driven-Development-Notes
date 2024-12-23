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
  - **Make it right:** Remove all duplication you have introduced/all code mess.
- As you refactor the code, you may realise that the interface you defined in the first step, isn't actually the best way to implement the required behaviour. As part of refactoring you can change the test to fit with your new understanding of how the interface should work.
- **How to approach TDD - 3 stratergies:**
  - **Fake it:** To get to green, return a constant. Then when refactoring gradually remove constants till you have real code.
  - **Use obvious implementation:** If there is an obvious solution, you can just implement this.
  - **Triangulation:** If you are struggling to see how to remove duplication, by adding more test cases it can help you generalise a problem.

### Chapter 3: Equality for All
- As you implement the code, new implied operations/functionality will be revealed. You can add those to the to-do list of tests.