# When to Mock Notes

- *These notes are on the article: https://blog.cleancoder.com/uncle-bob/2014/05/10/WhenToMock.html*
- *Note: Some of these ideas run contrary to ideas expressed by Ian Cooper. I included these notes to show the difference in beliefs around mocking.*

## The Extremes

- **If you used no mocks:**
  - Execution of test suite will likely be slow. Web servers/databases/services over network are often the bottleneck if you don't mock them out.
  - Test coverage likely to be low as it is very hard to test some situations without using mocks. For example error conditions
  - Tests are sensitive to faults in parts of system unrelated to what is being tested. Can make tests tricky to debug.
- **If you used too many mocks:**
  - Can make tests slower if you mock out a class with something slower than it.
  - Mocking interactions between all classes can cause setup code to become extremely complicated. It also means mocking structure becomes highly coupled to implementation details (making refactoring increasingly tricky).
  - Overall mocking too much leads to test suites that are slow, fragile, and over-complicated.

## Goldilocks Mocks - The Right Level of Mocking

- Heuristic: **Mock across significant architectural boundaries, but not within these boundaries**
  - This means mock:
    - Databases
    - Web servers
    - External Services
    - Significant architectural boundaries, which are enforced with interfaces (so you can independently develop on either side of your boundaries). These architectural boundaries form the separation of concerns for your program. You could consider these your "modules".
  - The benefits:
    - Tests run faster
    - Tests not sensitive to failures of mocked out components
    - Easy to test failure scenarios
    - You generally don't create mocks that return other mocks, so setup remains cleaner.
- Heuristic: **Write your own mocks**
  - Writing mocks across architectural boundaries is easy as you have a clearly defined interface.
  -  It forces you to design and organise your mocking structure
  - When you write your own mocks they are going to be fast
- Heuristic: **Mock sparingly:**
  - By reserving mocking for architecturally significant boundaries you will keep mocking to a minimum.
  - If you find within an architectural boundary you need a mock to test, find a way to design the system so this isn't needed.

  ## Extra Notes
  - *These are some ideas I had on this article.*
  - In the context of this article, we can apply the standard testing pyramid:
    - Unit Tests: Test a single module in isolation
    - Integration Tests: Test the integration of two or more modules. Also test the integration between modules and external dependencies like databases or external HTTP APIs.
    - E2E Tests: Test the whole system (so all modules together, including the UI)