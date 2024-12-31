# TDD, Where Did it All Go Wrong
- Talk by Ian Cooper: https://youtu.be/EZ05e7EMOLM?si=53gJ6EMpQ6IF2WqL

## The Problem

- When you want to change some of the code, it breaks a lot of tests. When you refactor, even though you aren't changing the behaviour of the code, tests still break. This especially occurred in heavily mocked tests.
- TDD slows developers down. Instead the "duct tape programmer" outperforms in the eye's of business owners because they write awful code but quickly, so features get shipped.
- When you go back to tests when they are broken, you don't understand their intent. This especially occurs with tests with lots of mocks.
- Tests can end up just testing mocks when mocks are excessively used.
-  ATDD suites (Acceptance Test Driven Development) are where you write high-level system requirements using tools like Gherkin so customers can read these tests in natural english. However it took a huge amount of work to maintain, and the customer never looked at them. The ATDD suites were  slow to run, and developers ended up ignoring them because they would almost always end up being red.

## The solution

- Avoid testing implementation details, test behaviors that you want the system to implement.
- Many practice TDD by using 'adding a new method to a class' as the trigger to writing a test. The trigger for adding a new test, is that you have a requirement you want to implement.
- Test the public API of your software. It is the contract your software has with the world, which will not change rapidly. How that public API is implemented will change. But what that software offers to consumers is what you should test. The public API is **not a HTTP API, it is the exports from a module.** It is the publicly exposed area of your module.
- We should add tests to cover the uses cases or stories.
- The System Under Test is not a class. The system under test is the 'exports' from a module - its facade.
- The unit in unit testing is a module. A class may the be facade, but many classes are implementation details of the module.
- Heavy mocking leads to overspecified tests, as by specifying the mocks your tests start to know too much about the implementation.
- Write tests only against the stable contract of the API (the exports of your module).
- You can probe implementation details in tests if it helps you develop your software, but delete those tests after.
- The object of TDD is to test behaviour in the system
- Tests define what kind of external API you want for your test. The test comes the first consumer of your code that defines the best possible scenario for your API.
- The unit of isolation in TDD is the test (not the class under test). You don't have to have the class isolated, you just need to have tests that run independently from one another.
- We may choose to avoid file systems/databases via mocking to stop tests affecting each other. It also helps speed up our tests. But if these aren't problems then there are no problems with unit tests calling databases.
- TDD unit tests focus on a story of a behaviour that the system should implement.
- If a test is simply testing a method, it can be tricky for us to understand what it is doing. However, if a test tests a behaviour that can make it much easier to understand because behaviours make sense to us.
- **Red-Green-Refactor:** Write a little test that doesn't work (make sure that the test doesn't always pass). Make the test work quickly, committing whatever sins necessary (you can just cut and past code from stack overflow). Then in refactor eliminate all duplication. In the green stage speed trumps design. The refactoring step is when we produce clean code. When you refactor, you do not write any new tests (you aren't changing behaviour, you are just changing the design of the code). In refactoring you don't implement any new part of the public API.
- Dependency is the key problem in software development at all scales. Try to decouple by focusing on your stable public contract (the public API) and not implementation details. This allows us to refactor without breaking tests.
- Test behaviours not implementations
- Don't test internals
- Don't make everything public in order to test it. Things shouldn't be public unless they are part of the public API.
- "Refactoring is the process of changing a software system in such way that it does not alter the external behaviour of the code yet improves its internal structure."
- Testing Pyramid (From most to least):
  - Majority of testing should be unit tests which each test a single module
  - Integration Tests: Tests which check different modules work together.
  - UI Tests: Tests which run on your UI
- Hexagon Architecture: In center of architecture are plain objects, and then on outside is adapter layer which knows how to work to the rest of the world. Then in between these, it is the ports layer which is a facade layer. The port is the ideal point for tests (as this is where things talk to the database).
- Integration tests just check that you can talk to the adapters correctly
- Gears: You can move quicker or slower with testing.
- ATDD: Don't do it because customers don't participate and create a significant maintenance burden. When your TDD practices are about behaviours, then the main benefits of ATDD (which are testing behaviours) are there without all the negatives.
- Mocks are useful when a resource is expensive to create.
- Summary:
  - The reason to test is a new behaviour, not a method on a class
  - Write dirty code to get to green, the refactor
  - No new tests for refactored internals and privates (methods/classes). As in refactoring you are only changing the design, not the behaviour of the system. If you only write tests to target new behaviours, refactoring will therefore need no new tests to accepts
  - Both Develop and Accept against tests written on a port
  - Add integration tests for coverage of ports to adapters
  - Add system tests for end-to-end confidence
  - Don't mock internals, privates, or adapters