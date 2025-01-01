# Test-Driven Development By Example - Summary

## TDD Core Principles

- **TDD Goal:** Make clean code that works.
- **Two Commandments of TDD:**
  - Write new code only if an automated test has failed
  - Eliminate duplication
- **Red - Green - Refactor:** The cycle followed in TDD for each test, after which you follow the same cycle for the next test, and so on:
  - **Red:** Write a test that doesn't work (not working includes not compiling). This test acts as the "story" of the interface you wished you had. Run the test before coding to check it isn't already working.
  - **Green:** Make the test work (speed dominates everything else in this phase).
  - **Refactor:** Eliminate duplication/mess created in the green stage. Duplication includes duplication between test and code.
- **Test To-Do List:** Maintain a to-do list of test cases you want to implement. When you think of a new test case at it to the list, and then return to working on your current test. 
- **How to approach TDD - 3 strategies:**
  - **Fake it:** To get to green, have your methods return the constants required by the test. This creates duplication of these constant values between the test and code. So gradually remove constants and replace them with real code till you arrive at a proper implementation.
  - **Use obvious implementation:** If there is an obvious solution, you can just implement it.
  - **Triangulation:** If the two previous approaches failed, add more examples to your test. By having more examples it can help generalise a problem. Then when you solve the problem, remove unnecessary extra examples.

## TDD Pros + Cons

- **TDD Benefits:**
  - Reduces defect density
  - Allows us to be confident in our programming, when you make a change if all the tests still pass you know you haven't introduced any new defects.
- **TDD Limitations:** TDD doesn't solve all your problems, other forms of testing are still required, like:
  - Performance Testing
  - Stress Testing
  - Usability Testing

## Writing Tests

- **Decouple tests and code:** Tests should only use the public API of the unit you are testing.
- **Development Tests:** When you don't know how to tackle a test you can start with a series of "development tests" working up to solving it. Then when you get the original test working you can delete the interim "development tests" that you used to get there.
- **If it isn't tested, it might break:** When refactoring you will come across edge-cases/areas where the code isn't tested. Write tests retroactively to cover these areas.
- **Given, When, Then:** This is a format for writing tests(also known as Arrange, Act, Assert).
  - **Given:** Create some objects
  - **When:** Perform some operations on the objects
  - **Then:** Check the results are correct
- **Test Isolation:** Success/failure of one test should be independent of the success/failure of another. Therefore tests shouldn't share objects. To do this easily you need to break your solution into many highly cohesive, loosely coupled objects which can easily be set up for each test.
- **Assert First:** When writing tests, start by writing the asserts. Then you can work backwards to fill out the rest of the test.
- **Test Data:**
  - Use minimal amount of test data necessary to check all different cases
  - Never use same constant twice (unless the constant means the same thing), as this can cause confusion.
  - Try make the connection between numbers used in test data obvious (perhaps by writing out the calculation to get from input to output data)
- **Mocks:** To test a unit that relies on a expensive/complicate resource you can create a fake version of that resource which returns pre-defined responses. Common example of a dependency that needs mocking is a database.
  - **Crash Test Dummy:** A fake object/mock which returns an error from one of its methods, used to test error handling code.
- **Fixtures:** Used to reduce duplication of setting objects up
- **When to delete tests:**  You can delete tests if they don't increase your confidence in the system (because what it is testing is already covered by a different test) and if it isn't communicating something new to the reader.

## TDD Workflow Tips

- **Step Size:** In TDD we generally take small steps. This helps us to move confidently with tricky problems as we are only making small changes each time. This applies to both making a test work (if a test is too big to tackle at once, split it into smaller sub-tests), and refactoring. The changes we make should only be to a few lines at a time. However we can always move to a "higher gear" and make bigger changes at once when we are feeling confident.
- **Work on one test at once:** Try not to add new tests when a current test is failing. If you find that you need to, rollback to the last state all tests worked and then add the new required test.
- **Start Simple:** When implementing a new operation, start with the simplest test possible. Often this is making a test for a trivially easy version of the operation/a version of the operation that does nothing. For example with a method that adds to a value, test adding 0.
- **Learning Tests:** When using an API you didn't develop, as part of learning the API create tests which verify how the API works. This teaches you how to use the software, and if a new version of the software is released you can run the tests to verify the code works the same way.
- **Do over:** Don't be afraid to just start over. If you've made a complete mess, sometimes the quickest way forward is by starting from a blank slate with all the new knowledge you have.

## Refactoring Techniques

- **Reconcile Differences:** If you have two elements which look similar, slowly make little changes to bring them closer together. When they are identical you can merge/delete one to reduce duplication.
- **Isolate Change:** When you need to change one part of a multi-part method/object isolate it first to make it easy to change (can be done with techniques like *Extract Method* or *Method Object*).
- **Extract Method:** To make a long/complicated method easier to read, turn a small part of the method into a separate method and call the new method.
- **Inline Method:** The opposite of extract method, used when you are struggling to see how to move forward refactoring when code is scattered across the code base. You replace method invocations with the method code itself. This can bring all the code to one place, so it is easy to see how to move forward.
- **Method Object:** To represent a complicated method that requires several parameters/local variables, you can make an object out of the method. This also lets you swap out and plug in new computations easily (by swapping the method object).

## How to check if your doing it right:

- **Measurements of test quality:**
  - **Statement Coverage:** Should be close to 100% if TDD followed religiously. Can be improved either by writing more tests or simplifying code (so existing tests cover more code).
  - **Defect Insertion:** Method of automatically inserting errors into code and checking if tests catch it (by failing). Also known as mutation testing.
- **Signs of Bad Tests/Bad Code:**
  - **Long setup code:** If you have to spend hundreds of line creating objects from a simple assertion, your objects might be too big and need to be split (so individual parts can be tested easily).
  - **Setup duplication:** If you can't easily find a common place for common setup code, then there are too many objects too tightly coupled.
  - **Long running tests:** TDD tests that take a long time to run, won't get run (defeating the point of TDD). This often occurs because you can't test parts of the design and have to setup/tear down the full thing each time.
  - **Fragile tests:** Tests the break unexpectedly occur if parts of your program that should be separate actually have some connection.