# TDD, Where Did it All Go Wrong
- Talk by Ian Cooper: https://youtu.be/EZ05e7EMOLM?si=53gJ6EMpQ6IF2WqL

## Test behaviours not implementations

### Problem

- Tests become too coupled with internal code details, so the tests become a drag on refactoring. This especially occurs due to heavy mocking.

### Solution

- **Test behaviours not implementations**
- Instead of testing implementation details, test behaviours.
- The trigger for adding a new test, is that you have a new behaviour/use case you want to implement.
- Test the "public API" of your software, this is the publicly exposed contract that the software offers to consumers. (*Note: Public API doesn't mean HTTP API, it's just the exports from a module.*)
- The System Under Test is the "exports from a module" where the module could include many classes
- By writing your tests, you define what the external API of your code should do.
- You shouldn't make parts of your system public to test them. The tests should be reflecting the behaviour you want your system to have, you shouldn't be altering your systems behaviour for the tests.
- Try not to use mocking, when you could just use the actual implementation instead. Mocks can tie tests to implementation details, which means we try and minimise their use.
- Some mocking may need to be used to avoid using slow resources/resources which make it hard for tests to run in isolation. Classic example for this are databases or file systems. However, if you can find a way to test these external elements without mocking, there are no rules saying that you aren't allowed to.

## Development with the Red-Green-Refactor Loop

### Problem

- TDD can slow programmers down (due to the slow writing of tests).

### Solution

- **Red-Green-Refactor:**
  - **Red:**Write a test that doesn't work which specifies some new behaviour the system should have (and run it to ensure this test fails).
  - **Green:** Make the test succeed ("go green") as quickly as possible. Don't worry about good design, just get it to work. This gives you the speed to move quickly.
  - **Refactor:** Eliminate duplication/reduce code smells/apply patterns to make the code clean. In the refactor step you aren't changing/adding any behaviours, you are merely changing the design of code which enables that behaviour. As tests specify the system's behaviour, the tests shouldn't change/you shouldn't add any tests in this step.

## Testing Pyramid

- We use different types of testing, ordered from which tests should be most prevalent to least prevalent:
  - Unit Tests: These are the tests you will mostly be writing when you create your developer tests in TDD. They each test a single module.
  - Integration Tests: These test check that different modules integrate together correctly. They also can be used to check that your code integrates correctly with external I/O services (such as databases, or HTTP API's that the code calls).
  - UI (or E2E) tests: These tests run on your UI and make sure the whole system works correctly.

## Hexagonal Architecture

- At the core of the architecture is a group of plain objects holding your business logic.
- On the outside is the adapter layer, which talk to outside services such as the UI, databases, HTTP adapter (such as Flask), etc.
- The core is then connected to these adapters via ports. This is some kind of "facade" layer.
- The port is often a good place to test the system, as this is where outside consumers "talk" to the system.
- Integration tests check that you can talk to the adapters correctly.

## Gears

- You can move quicker/slower using TDD.
- When you are confident, you can move to a "high" gear. Instead of writing bad code and then refactoring it, if you already know the correct code you can just write it first time round. You can move in bigger steps.
- But if you are un-confident/moving in big steps isn't working, then you can slow down. You can even write tests which can help you along the way (which can check implementation details), but then delete them afterwards.

## ATDD (Acceptance Test Driven Development)

- ATDD is where tests are written from a users perspective, often in plain English. This plain english is than transformed into a test by a testing framework (such as Gherkin or FitNesse). These high level tests then motivate development.
- These don't work because:
  - Customers aren't interested
  - They take a lot of effort to maintain
  - They stay red for most of the development cycle (as a feature hasn't been implemented yet). This means developers begin to ignore red acceptance tests, so if tests begin to go red because a bug has been introduced people just ignore it.
- Previously they were used to check the behaviour of the system is correct. But we now test the behaviour of the system is correct with our tests using TDD, so acceptance tests are no longer needed.

## Summary

- *These summary notes have been taken from the talk slides.*
-The reason to test is a new behaviour, not a method on a class
- Write dirty code to get to green, the refactor
- No new tests for refactored internals and privates (methods/classes). As in refactoring you are only changing the design, not the behaviour of the system. If you only write tests to target new behaviours, refactoring will therefore need no new tests to accepts
- Both Develop and Accept against tests written on a port
- Add integration tests for coverage of ports to adapters
- Add system tests for end-to-end confidence
- Don't mock internals, privates, or adapters