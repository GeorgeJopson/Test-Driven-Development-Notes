# TDD, Where Did it All Go Wrong
- Talk by Ian Cooper: https://youtu.be/EZ05e7EMOLM?si=53gJ6EMpQ6IF2WqL

## The Problem

- When you want to change some of the code, it breaks a lot of tests. When you refactor, even though you aren't changing the behaviour of the code, tests still break. This especially occurred in heavily mocked tests.
- TDD slows developers down. Instead the "duct tape programmer" outperforms in the eye's of business owners because they write awful code but quickly, so features get shipped.
- When you go back to tests when they are broken, you don't understand their intent. This especially occurs with tests with lots of mocks.
- Tests can end up just testing mocks when mocks are excessively used.
-  ATDD suites (Acceptance Test Driven Development) are where you write high-level system requirements using tools like Gherkin so customers can read these tests in natural english. However it took a huge amount of work to maintain, and the customer never looked at them. The ATDD suites were  slow to run, and developers ended up ignoring them because they would almost always end up being red.

## The solution

- Avoid testing implementation details, test behaviors
- Many practice TDD by using 'adding a new method to a class' as the trigger to writing a test. The trigger for adding a new test, is that you have a requirement you want to implement.
- Test the public API of your software. It is the contract your software has with the world, which will not change rapidly. How that public API is implemented will change. But what that software offers to consumers is what you should test. The public API is **not a HTTP API, it is the exports from a module.** It is the publicly exposed area of your module.
- We should add tests to cover the uses cases or stories.
- The System Under Test is not a class. The system under test is the 'exports' from a module - its facade.
- The unit in unit testing is a module. A class may the be facade, but many classes are implementation details of the module.