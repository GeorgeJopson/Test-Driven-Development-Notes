# TDD Revisited - Notes

- Talk by Ian Cooper: https://youtu.be/IN9lftH0cJc?si=GoBXlKVwLQi8jfOb

- **Fallacy:** Developers write Unit Test
  - TDD has nothing to do with unit tests.
  - **Unit test:** To isolate issues that may arise, each test case should be tested independently. Substitutes such as method stubs, mock objects, fakes, and test harnesses can be used to assist testing a module in isolation.
  - We used to test modules (module nebulously defined as a class or something much bigger). The module was treated as a black box, and the test probed from the outside. You wanted to check that any errors that test had was inside the box, so you'd replace dependencies with a fake/substitute. The thought was that modules should be separately tested (meaning tested in isolation), any dependency was mocked out.
  - This creates some problems. Firstly you have to know how you are partitioning your namespace first. You have to know how your code is going to fit together so that you can figure out where are these boundaries at which we mock. We have to design our class hierarchy to know what is the responsibility of another section of the design, so we know to mock it. This leads us to do upfront design (instead of letting tests inform our design). This means that now in our tests we understand the implementation details (because we need to know what the architectural boundaries are where we are mocking at). So you can't change this high-level design stuff without changing the tests.
  - When using mocks to replace our dependencies, it can lead to fragile tests. This is because mocks can cause overspecified software and behaviour sensitivity.
  - **Principle:** Developers write developer tests not "unit tests".
  - **Refactoring:** A change made to the internal structure of software to make it easier to understand/cheaper to modify without changing its observable behaviour.
  - We should only test the contract that your exposes the other callers.
  - If a program's behaviour is stable from an observer's perspective, no tests should change. 
  - "Tests should be coupled to the behaviour of code and decoupled from the structure of code." - Kent Beck
  - "My personal style is I just don't go very far down the mock path... your test is completely coupled to the implementation not the interface... of course you can't change anything without breaking the tests" - Kent Beck 
- Definition of Unit test - "Failure of unit test shall implicate one and only one unit. (A method, class, module, or package.)"
- Definition of Developer Tests: "Failure of a Programmer Test, under Test Driven Development, implicates only the most recent edit." - This means that you should only make small changes when developing with TDD, because if a test fails you don't automatically know what failed it. (This links with the idea of driving in "gears".) If you find your hitting the debugger a lot, your making too big a jump.
- It is your choice to decide where to put these tests, if you go high level (test from HTTP API for example) then you could use.
- Hardcore TDD folks say that if you add code and then the tests break, delete the code and try again. The reason they had this rule is to not write 200 hundred lines of code.
- Test Driven Development produces Developer Tests. The failure of a test case implicates only the developer's most recent edit. This implies that developers don't need to use Mock Objects to split all their code up into testable units. And it implies a developer may always avoid debugging by reverting that last edit.
- Don't use mocks to isolate the SUT when doing Developer Tests.
- Tests are isolated from each other, this means they can run in parallel (so they can be fast). The most common reason for interference is a shared state (aka shared fixtures). We mock shared fixtures to allow tests to work in parallel. I/O is the most common shared fixture (such as databases or resources that we access over a network). We also use mocks for I/O due to speed.
- You only test the public interface other people depend upon.
- **Principle:** The trigger for a new test is a new behaviour.
- TDD is about a contract-first technique for exploring how an API solving requirements
- The next tests you write in TDD is just the most obvious step that you can make towards implementing the requirement given by the use case or user story
- "Customers illustrate their descriptions with concrete examples... programmers use these examples to guide their work... Sometimes (programmers) use the examples directly in their tests... More often... programmers use the examples as a guide, writing a multitude of more focused, programmer-centric tests as they use TDD."
- Testing afterwards leads to upfront design. If you are writing code that isn't need by the given requirements (as in, not driven by the tests) you are engaging in speculation. Most likely you will be wrong, and you will have to delete or re-work that code.
- TDD followed religiously should have 100% code coverage. This is because all code is motivated by a test, so you are never writing code that isn't motivated.
- **Observation:** TDD is useful where it can provide fast binary feedback. If it is not the fastest way to provide feedback, use something else.
- New testing pyramid:
![New Test Pyramid](TestPyramid.png)
  - Developer tests check the behaviour of the system
  - Where you need to check integration with I/O systems work, or implement end-to-end tests, then a more classical automated testing approach works
  - Then monitoring and alerting through logs
  - Manual Tests