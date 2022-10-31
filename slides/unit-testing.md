---
layout: presentation
title: Unit Testing
permalink: /slides/unit-testing/
---

class: center, middle

# Unit Testing

Validating the behavior of functions.

---

# Agenda

1. [Overview](#overview)
2. [Example](#example)
3. [Advantages](#advantages)
4. [Test Cases](#test-cases)
5. [Assertions](#assertions)
6. [Best Practices](#best-practices)
7. [Doubles](#doubles)
8. [Javascript Testing Toolset](#tools)
9. [Conclusions](#conclusions)

---

name: overview

# Overview

--

## Concept

A unit is the smallest testable unit of code - typically a function, but sometimes an object or class.

--

- Unit testing verifies that each unit behaves as expected, given specific inputs.

---

template: overview

## Background

Unit testing is an automated testing technique developed in 1992 by Kent Beck to solve the annoyance of manually testing code for obvious errors.

--

- originally written in Smalltalk

--

- JUnit created by Beck as a way to teach himself Java during the course of an airplane flight from Zurich to Upsalla in 1997

--

- shared with Martin Fowler, a fellow signatory with Beck of the Agile Manifesto, who helped spread it

--

- now ported to just about every high-level programming language

---

template: overview

## Other languages

The world of unit testing frameworks for different languages that are based on the original JUnit is called **xUnit**.

--

- all open source, since JUnit was released open source

--

- all written in the same language that they are testing

---

name: advantages

# Advantages

--

## Comparison to Alternative

Automated unit testing has many advantages over manual debugging:

--

- less time consuming and tedious

--

- requires fewer human resources

--

- provides immediate feedback of failures

--

- allows developers to focus more on writing code

--

- more reliable than manual testing

---

template: advantages

## Relationship to Refactoring

Refactoring of existing code involves rewriting it to make it better organized and efficient without changing its observable behavior.

--

- It is often necessary to refactor code to make it more easily tested with unit tests - keep each function short and focused on a single task.

--

- With automated unit testing, refactoring will not accidentally introduce errors, since any such errors that change the behavior of the code will be immediately detected by the tests (called regression tests in this context).

--

> In almost all cases, I’m opposed to setting aside time for refactoring."
>
> -[Martin Fowler](https://martinfowler.com/), author of 'Refactoring', the book

---

name: examples

# Examples

--

## Java

A unit test example in Java using JUnit:

--

```java
// include JUnit and assertion libraray
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class MyFirstTest {

    @Test
    public void multiplicationOfZeroIntegersShouldReturnZero() {
        MyClass tester = new MyClass(); // MyClass is tested

        // assert statements for a variety of test cases
        assertEquals(0, tester.multiply(10, 0), "10 x 0 must be 0");
        assertEquals(0, tester.multiply(0, 10), "0 x 10 must be 0");
        assertEquals(0, tester.multiply(0, 0), "0 x 0 must be 0");
    }
}
```

---

template: examples

## Javascript

A unit test example in Javascript using `mocha`:

--

```javascript
// use mocha's built-in assertion library
const assert = require("assert")

// a set of tests of array functions
describe("Array", function () {
  // one particular unit test
  describe("#indexOf()", function () {
    // assert what should be returned
    it("should return -1 when the value is not present", function () {
      // test that assertion
      assert.equal(-1, [1, 2, 3].indexOf(4))
    })
  })
})
```

--

If the project's `package.json` file is set up with a script called `test` that contains the command to execute the tests using, then the tests can be run from the same directory as the `package.json` file with `npm test`.

---

template: examples

## Javascript (continued)

A unit test example of a back-end route using `mocha`, `chai`, and the [chai-http](https://www.chaijs.com/plugins/chai-http/) extension for simple testing of routes.

--

```javascript
describe("GET request to /foo route", () => {
  it("it should respond with an HTTP 200 status code and an object in the response body", done => {
    chai
      .request(server)
      .get("/foo")
      .end((err, res) => {
        res.should.have.status(200) // use should to make BDD-style assertions
        res.body.should.be.a("object") // our route sends back an object
        res.body.should.have.property("success", true) // a way to check the exact value of a property of the response object
        done() // resolve the Promise that these tests create so mocha can move on
      })
  })
})
```

---

template: examples

## Python

A unit test example in Python using `pytest`:

--

```python
import pytest
from some_package import some_module

class Tests:

  def test_some_function(self):
    '''
    Verify some_function() returns a non-empty string.
    '''
    actual = some_module.some_function() # get the actual return value of the function
    assert isinstance(actual, str), f"Expected some_function() to return a string. Instead, it returned {actual}"
    assert len(actual) > 0, f"Expected some_function() not to be empty. Instead, it returned a string with {len(actual)} characters"

```

--

Note that `pytest` works best when all test files are in a `tests` directory with filenames that start with `test_` and all test functions start with `test_`.

- just run the command `python3 -m pytest` from the main project directory to run all tests.

---

template: examples

## Python (continued)

A unit test example of a back-end route using the [pytest-flask](https://pytest-flask.readthedocs.io/en/latest/index.html) extension for simple testing of routes.

--

```python
import pytest
from project import create_app

class Tests:

  def test_foo(self):
      app = create_app('flask_test.cfg') # this method must be defined in production code and must return the flask app object
      with app.test_client() as test_client:
          response = test_client.get('/foo')
          assert response.status_code == 200 "/foo should respond with an HTTP 200 status code"
          response_obj = json.loads(response.data.decode('utf8')) # convert json response body data into an object
          assert response_obj.success == True, "Expected the response object to have a property 'success' with value True"
```

---

name: test-cases

# Test Cases

--

## Minimal Number

Unit tests must test at least two scenarios, called **test cases**:

--

- test the expected output when given valid input

--

- test the expected output when given invalid input

--

In actuality, there will usually be **many test cases** per production function for every possible variety of valid and invalid input.

---

name: assertions

# Assertions

--

## Concept

Every unit testing framework depends upon a set of **assertions** - purported truths that are then compared against reality.

--

- An assertion is a statement that a particular predicate is going to be true - this is either true or false.

--

- If false, the assertion fails and throws an error about what went wrong and where that happened in code

---

template: assertions
name: assertions-1

## Typical Assertions

This is a partial list of methods in **JUnit's asssertion library** that all other testing frameworks tend to imitate:

--

### Equality:

- `assertEquals(primitive/object expected, primitive/object actual)`
- `assertNotEquals(primitive/object expected, primitive/object actual)`
- `assertArrayEquals(expectedArray, actualArray)`

---

template: assertions-1

### Truth:

- `assertTrue(boolean condition)`
- `assertFalse(boolean condition)`

---

template: assertions-1

### Existence:

- `assertNull(Object object)`
- `assertNotNull(Object object)`

---

template: assertions-1

### Sameness:

- `assertSame(object1, object2)`
- `assertNotSame(object1, object2)`

---

name: best-practices

# Best Practices

--

## TRIPinesss

According to "[Pragmatic Unit Testing in Java with JUnit](https://pragprog.com/titles/utj/pragmatic-unit-testing-in-java-with-junit)", by Andy Hunt and Dave Thoma, good unit tests are **TRIP-y**:

--

- **T**horough

--

- **R**epeatable

--

- **I**ndependent

--

- **P**rofessional

---

template: best-practices

## Three pillars

According to Roy Osherove, author of "[The Art of Unit Testing](https://www.manning.com/books/the-art-of-unit-testing)", there are three main pillars of a good unit test:

--

- **Trustworthiness** - if you don't believe your test, and find yourself verifying it or ignoring it, it's a sign you should rewrite it.

--

- **Maintainability** - a test that is difficult to maintain and takes up more time than it saves might as well be scrapped

--

- **Readability** - a test that is not obvious as to what it's testing is a bad test. Tests serve as a form of documentation.

--

Listen to [a song about unit testing](https://www.youtube.com/watch?v=fXwWaE1QCS8) by Roy Osherove

---

name: doubles

# Doubles

--

## Concept

Unit tests must run in isolation of one another and of external dependencies, such as databases, APIs, or other servers.

--

- Some units of production code normally depends upon an interaction with such a dependency. What to do?

--

- Swap out that dependency with the double! - a controlled simulation of the dependency.

--

- Using a double will allow you to hone in on problems with your own code, not problems within the external dependency.

---

template: doubles

## Types of double

There are three commonly-used types of doubles.

--

- Mocks

--

- Fakes

--

- Stubs

---

template: doubles

## Mocks

Mocks are replacements for external interfaces.

--

- The mock assumes the same name and functions as the mocked external dependency.

--

- Using a mock can determine only whether the mock has been called or not by production code, how many times it has been called, and whether or not the correct arguments are passed to it when it is called.

--

- Production code does not need to be changed to use a mock. It does not "know" that it is not connecting to the real thing.

--

- The testing framework takes care of swapping out the external dependency with a mock.

---

template: doubles

## Stubs

Whereas mocks are called by production code and passed arguments in place of a real external dependency, stubs are used to return pre-defined responses to the calling code.

--

- For example, if your app code requires a record to be saved in a database, you might create a mock to intercept the arguments that would normally be sent to the database in place of the real thing, and create a stub that responds with a success or failure message in place of the real response that the database would send, given the supplied parameters.

--

- Having a mock send back a stub allows you to use unit tests to determine whether your production code handles the response correctly.

---

template: doubles

## Fakes

Like, mocks and stubs, fakes are used in the simulation of an external dependency. But whereas mocks and stubs are simple code substitutions for the real thing, a fake is an actually functioning replacement for the external dependency that runs on the local machine.

--

- For example, if your code must connect to an API over the Internet, you might create a local HTTP server that simulates that API as your fake so you can test as if it were real.

--

- Since unit tests must run independently of one another, any data sent back and forth with the fake will not be saved and will not influence subsequent unit tests that interact with the fake - there is no saved state within the fake.

--

- The advantage of using fakes over mocks and stubs is that you get a slightly more "real" test.

---

name: tools

# Testing Tools

--

## Javascript

The following are the recommended tools for unit testing in Node.js Javascript.

--

- [mocha](https://www.npmjs.com/package/mocha) as the Javascript testing framework.

--

- [chai](https://www.npmjs.com/package/chai) as the assertion library.

--

- [chai-htp](https://www.chaijs.com/plugins/chai-http/) - an extension to `chai` that simplifies testing of express.js routes.

--

- [istanbul / nyc](https://www.npmjs.com/package/nyc) for code coverage analysis.

--

- [sinon](https://www.npmjs.com/package/sinon) for stubs, mocks, and fakes.

--

- [faker](https://www.npmjs.com/package/faker) for any placeholder data that needs to be generated in tests (e.g. names, email addresses, database data, images, etc)

---

template: tools

## Javascript (continued)

- To learn more about refactoring your code to be suitable for unit testing, watch the LinkedIn Learning video "[Prepare for Testing](https://www.linkedin.com/learning/node-js-essential-training-web-servers-tests-and-deployment/prepare-for-testing)"

--

- To master the syntax of `mocha` and `chai`, watch the "[Writing Unit Tests](https://www.linkedin.com/learning/javascript-test-driven-development-es6/the-purpose-of-unit-testing?u=2131553)" section of videos in the LinkedIn Learning Course, "Javascript: Test-Driven Development".

--

- Add `istanbul`'s code coverage tool, `nyc`, following [this StackOverflow discussion](https://stackoverflow.com/questions/16633246/code-coverage-with-mocha).

--

- Learn how to make doubles with `sinon` by watching [this video](https://www.youtube.com/watch?v=Qlmv7nox5pM) from the Grace Hopper Full Stack Academy, and reading its [documentation](https://sinonjs.org/#get-started).

---

template: tools

## Python

The following are the recommended tools for unit testing in Python.

--

- [pytest](https://docs.pytest.org/en/7.2.x/) as the Python testing framework.

--

- [pytest-flask](https://pytest-flask.readthedocs.io/en/latest/) - a module that helps test flask routes using pytest

--

- [coverage](https://coverage.readthedocs.io/en/latest/) for code coverage analysis.

--

- [monkeypatch](https://docs.pytest.org/en/6.2.x/monkeypatch.html) for mocking and faking.

--

Documentation on each of these sites is reasonably good.

---

template: tools

## Python (continued)

- To learn more about unit testing in Python, watch the LinkedIn Learning video "[Unit Testing and Test Driven Development](https://www.linkedin.com/learning/unit-testing-and-test-driven-development-in-python/welcome?autoplay=true&u=2131553)"

---

name: conclusions

# Conclusions

--

This slide deck has attempted to give you a high-level overview of the intentions and directions of unit testing. Now go and try it.

- Thank you. Bye.

```

```
