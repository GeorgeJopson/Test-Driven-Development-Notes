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
- When you write a test you are testing the API of some piece of code. Write the test imagining the perfect API of how you want the feature implemented. 
- By creating a test, you create a dependency between the test and the code. By reducing duplication as much as possible, you can help eliminate dependencies as much as possible.
- In the refactor step, you can take many small steps of refactoring (each time ensuring the tests are still green).

### Chapter 2: Degenerate Objects

-  TDD cycle:
  - **Write a test:** Write a "story" of the interface you wish you had, and the outputs of that interface
  - **Make it run:** Quickly get the bar to go green. Speed dominates everything else in this phase.
  - **Make it right:** Remove all duplication you have introduced/all code mess. This includes duplication between test and code.
- As you refactor the code, you may realise that the interface you defined in the first step, isn't actually the best way to implement the required behaviour. As part of refactoring you can change the test to fit with your new understanding of how the interface should work.
- **How to approach TDD - 3 strategies:**
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

- With tests, instead of reasoning about whether something will work, you can empirically find the answer by running the tests.
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

- Refactoring pattern: Hard-wire your code to work for one instance and then generalise it to work with all instances by replacing constants with variables.
  - This is an advantage of TDD, you can start by implementing concrete examples you know work, and then generalising from there (instead of having to jump directly to the generalised example).
- Don't be afraid to work in tiny steps (only changing a handful of lines at a time).

### Chapter 19: Set the Table

- 3A framework for writing tests (also know as **given, when, then**):
  - **Arrange:** Create some objects
  - **Act:** Stimulate them
  - **Assert:** Check the results are correct
- The first step **arrange** is often the same from test to test
- **Isolation** is key for tests, the success/failure of one test should be irrelevant to other tests.
  - Therefore, tests shouldn't share anything so objects should be recreated for each test that use them.

## Part III: Patterns for Test-Driven Development

### Chapter 25: Test-Driven Development Patterns

- By testing you reduce stress because you know you haven't broken anything.
- You should run your test after you write it, because even if you think it is going to fail you might be wrong (maybe your system already accounts for the tested feature).
- Tests should be so fast that you can run them yourself and run them often. Then you can catch errors quickly.
- **Isolated Tests:** Tests should be independent from each other.
  - To have isolated tests you need to break your problem into many highly cohesive, loosely coupled objects which can then easily (and quickly) be set up for each test.
- **Test List:** Before you begin, write a list of all the tests you will have to write. You can then add items to the list as you gain knowledge about the system.
Add each operation you want to implement (along with each case of that) and then refactorings you think you will need to do.
- When you write a test, the next step is to implement it. Don't write all your tests at once as by getting a test to work you gain more knowledge which might help you write the next test. It also is a more interesting way to work.
- Conservative TDD says that you should never be more than one change away from all your tests running.
- **Test First:** Write your tests first. It can clarify in your head what you are doing, and give you a method for scope control.
- **Assert First:** When writing your tests, start by writing the asserts. Then you can work back from what the asserts need to check to fill out the test.
- **Test Data:** 
  - Use the minimal amount of test data necessary to check all the different cases.
  - Never use the same constant twice unless the constant means the same thing. For example if we were implementing divide, 3/2 is different from 2/3. But if I used 2/2 as a test case we wouldn't know if the divide operation got the 2's the right way round.
- **Evident Data:** Make the connection in the numbers used as test data obvious. If it is simple enough, writing out the calculation you did to get from the input to the output in the test is useful for other programmers to see how you got to the expected output.

### Chapter 26: Red Bar Patterns

- When deciding what test to implement next from your to-do list pick a test which will teach you something and you are confident you can implement.
- when you are implementing a new operation, start by making a test for that operation which doesn't do anything (for example if you are implementing the plus functionality then this would be adding 0). By starting with trivially easy inputs/outputs you minimise the number of problems you have to solve. This is especially useful for tricky problems.
- **Learning Tests:** When you are using an API from something you didn't develop (such as a library), you can create learning tests the verify the API works as expected. As part of learning the API you write these tests, but they can also be used to verify that when a new version of the 3rd party software releases it still works as before.
- **Do Over:** Sometimes it is better to just start over. If you've made a complete mess, sometimes by starting back at a clean slate with the new knowledge you've gained is the best way to make progress.

### Chapter 27: Testing Patterns

- **Child Test:** When you write a test case which is tricky to make succeed, break up the problem into components. Then you can write smaller tests which each focus on one component of the problem (which should be easier to tackle). Use this technique if you accidentally write a test case which is too big, so you can maintain the incremental red/green/refactor cycle (instead of getting stuck in a quagmire trying to get one big test case to work). Then once you have implemented all the components you can re-introduce the bigger test case (and delete the smaller "development" tests which helped you get there).
- **Mock Object:** To test an object that relies on an expensive/complicated resource, you can create a fake version of that resource which returns pre-defined responses. This improves performance and reliability. Common example of item that needs mocking = database.
  - If you want to use mock objects, you can't store the things you are mocking in global variables (or Singletons), as this makes it hard to inject the mock for your tests.
- **Log String:** To verify that the sequence in which messages are called is correct, you could use a log string. The program under test produces this log string (adding an piece of text each time it sends a message), and this is checked by the test.
- **Crash Test Dummy:** You pass in a "fake" object to code which returns an error when one of its methods is called. For example a file system can be replaced with a "fake" file system which will return errors. This lets you test error code.
- **Broken Test:** If you are programming alone and are finishing a coding session, leave the last test broken. This gives you a place to pick up next time. However if you are programming in a team, leave all tests running (so whoever picks up can start from a place of certainty).

### Chapter 28: Green Bar Patterns
- These are patterns to get your tests to go green quickly.
- **Fake It:** Just have your code return constants to get the test working quickly. Then in the refactoring step you get it to work more generally by eliminating duplication of data between the test and code:
  - This gives you a concrete end goal to work towards, which you can work back from
  - It lets you get to green quickly, so you can refactor with confidence
  - It gives you a clear problem to solve (scope control)
- **Triangulate:** If you have a situation where you have an operation you want to implement but you are not sure how to abstract the operation so it works on any case, implement two examples in the test case. By satisfying both examples you can arrive at this abstraction. Generally this takes more work than "Fake It" or "Obvious Implementation" because you have to add multiple examples (where all but one will have to be deleted to avoid unnecessary duplication). However, if you are struggling, having the two examples can help you come to an abstraction.
- **Obvious Implementation:** If you can already see an obvious, simple solution just implement it. However if this causes a test to fail, move back to one of the "Fake It" or "Triangulate" techniques. Implementing an solution straight from the get go is moving quickly, but in unsteady territory it is easier to "move down a gear" and go slower.
- **One to Many:** When implementing an operation which works on a collection of objects (for example a list/tuple/set/etc of objects), make it work with a single item first. Then when you have figured that out you can make it work for all the collection.

### Chapter 29: xUnit Patterns

- All tests should be written use only public protocol/the public API of the unit you are testing. This means you can refactor the implementation, without refactoring the test.
- Fixtures can be used to reduce duplication of setting objects up.

### Chapter 30: Design Patterns

- **Command:** A method can return an object, which when the "run" method (or something equivalent) is invoked does the computation. This lets you pass round the object and you can call the operation whenever you need.
- **Value Object:** An object where operations on the object always produce a new object (so the original object is never altered). This solves aliasing issues where there are multiple references to the same object in different parts of the program. Normally this can cause issues, as if the object is modified in one part of the program, then this could have unexpected side effects in other parts of the program. However with value objects, you know they are never going to change so this isn't a problem.
- **Null Object:** Some methods may return null instead of a real object, which causes many checks for null in the code. Instead of returning null, return a default "null object" which just has default behaviour.
- **Template Method:** Where a superclass contains a method written in terms of other methods, and then subclasses implement those methods in different ways. This "template method" has the gaps filled in by the subclass (as it defines the methods).
- **Pluggable Object:** You can eliminate duplication of conditionals by encapsulating variation. We have separate implementations of an interface for each option, and to choose one of these options we create it and store it. Then instead of having to create a conditional to select between each option, we just use the pre-created object.
- **Pluggable Selector:** A technique for enabling different behavior for specific instances by storing a reference to the method that the instance should call and dynamically invoking it. This approach avoids the need for subclassing when the only variation between instances is a single method. It simplifies the design by eliminating the overhead of creating multiple subclasses for minor differences in behavior.
- **Factory Method:** This is where you create new objects using a method instead of a constructor. The factory method will call a constructor to create an object, but can then do extra work before returning the object. It gives you more flexibility by introducing this level of indirection.
- **Imposter:** To introduce variation into a computation, you can introduce a new object implementing the same interface/protocol but a different implementation. This can be utilised in the common examples:
  - Null object - You can treat the absence of data the same as the presence of data.
  - Composite - You can treat a collection of objects the same as a single object.
- **Collecting Parameter:** To collect the results of an operation that is spread overall several objects, you can add a parameter to the operation which passes in an object where the results will be collected.
- **Singleton:** A way to implement global variables in a language without global variables. This is an ANTI-PATTERN and *should not be used!!!*

### Chapter 31: Refactoring

- In TDD the semantics (what the program does) is specified in the tests. Refactoring is where we change our code while keeping the semantics the same.
- You need to have enough tests to make sure that they specify the wanted semantics correctly. "It's no excuse to say, 'I knew there was a problem, but the tests all passed so I checked the code in.' Write more tests."
- Common refactoring methods:
  - **Reconcile Differences:** If you have two elements (e.g. two loop structures, two branches of a conditional, two methods, etc) which look similar, slowly make little changes to bring them closer together. Then when they are identical you can merge them/delete one. This iterative process of many small steps avoids the need to do big risky changes to eliminate duplication all at once.
  - **Isolate Change:** When you have to change one part of a multi-part method/object, first isolate the part that has to change. Then in isolation it is easy to change. This isolation can be done via methods like *Extract Method* or *Method Object*.
  - **Migrate Data:** When refactoring moving from one representation of data to another can be a big change. This is antithetical to TDD. So instead temporarily duplicate the data. For example when changing the API of some system you could use these incremental steps:
    - Add a parameter in the new format.
    - Translate from the new format parameter to old format internal representation
    - Delete old format parameter
    - Replace use of old format with new format
    - Delete old format.
  - **Extract Method:** To make a long complicated method easier to read, turn a small part into a separate method and call the new method. This also has the added benefit of reducing the scope of local variables.
  - **Inline Method:** Sometimes code can become too scattered across many different methods too easily see how you can move forward in refactoring. Inline method is simply where you replace a method invocation with the method code itself (basically the reverse of extract method). This lets you see everything in one place, so you can once again move forward with refactoring.
  - **Extract Interface:** This is used if you have an object but you want to create another implementation of those operations that object implements. Simply create an interface (extract an interface) which the original class implements. Then your new class can also use this interface.
  - **Move Method:** In some cases methods could be more suitable to be in a different class. A good time to be suspicious that this is the case is if you see more than one message being sent to another object in a method (perhaps the method would be better suited in the object that is being called so many times).
  - **Method Object:** "How do you represent a complicated method that requires several parameters and local variables? Make an object out of the method." This lets you swap out and plug in new computations easily (by simply swapping out the method object). 

### Chapter 32: Mastering TDD

- Unless you have reason to distrust it, don't test code from others.
- Signs of bad tests/bad design creating bad tests:
  - **Long setup code:** If you have to spend hundreds of line creating objects from a simple assertion, your objects might be too big and need to be split (so individual parts can be tested easily).
  - **Setup duplication:** If you can't easily find a common place for common setup code, then there are too many objects too tightly coupled.
  - **Long running tests:** TDD tests that take a long time to run, won't get run (defeating the point of TDD). This often occurs because you can't test parts of the design and have to setup/tear down the full thing each time.
  - **Fragile tests:** Tests the break unexpectedly occur if parts of your program that should be separate actually have some connection.
- You can delete tests if they don't increase your confidence in the system (because what it is testing is already covered by a different test) and if it isn't communicating something new to the reader.
- **Switching to TDD mid-way through a project:** Instead of trying to do a huge refactor and write tests for everything, we slowly add tests into the parts of the code we are working on. By implementing these changes into code as wo go along, slowly the system will begin to look "test-driven".
- Benefits of TDD:
  - Reduced defect rates (allowing less stressful programming)
  - Short cycles where you get feedback almost instantly (so ideas can be validates quickly)
  - Simple Design: You only code what you need to get the tests working, and you remove all duplication before moving on. This automatically moves you towards a simpler, more elegant design.