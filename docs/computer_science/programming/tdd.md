---
title: TDD
date: 2021-09-05
author: m0wer
---

Test-driven development (TDD) is a software development process consisting in
small development cycles. The goal is clean code that works.
Some advantages of this methodology are that it reduces stress in
the development process and produces functional code that is a pleasure to
work with.

# Motivation

Are you scared about modifying your code? Do you feel like you need a full
empty day to add some new functionality to not be interrupted in the process?

Didn't it happen to you that you started refactoring a simple part of code and
ended up lost and confused with changes in tens of different files
and the code not working anymore? This is
what happens to the Refactoring Cat:

![Refactor cat](refactoring_code_cat.gif)

If you want to avoid this, stick to small steps, keep refactoring and
functionality changes entirely separate.

Be like the Testing Goat, obey the testing goat:

![Testing Goat](testing_goat.jpg)

The Testing Goat might be less smart than the Refactoring Cat, but it can reach
higher peeks just by going step by step.

Programming is hard, TDD helps keeping it simple so that you don't have to
make extra thinking efforts all the time. It let's you save your progress,
take a break, and make sure you never slip backwards.

# Getting started

TDD is a discipline. To get started, try doing a kata every day:
[Kata - The only way to learn TDD - Peter Provost's Geek Noise](http://www.peterprovost.org/blog/2012/05/02/kata-the-only-way-to-learn-tdd/).

# Development cycle

1. Write a test.
1. Run the tests and check that the new test fails.
1. Make the minimum code change to address the current test failure.
1. Run the tests and check that all pass.
1. Refactor the code (improve clarity, performance…). Use the tests to help you
  validate the changes.

One of this cycles might have subcycles. For example, if you want to add a new
high level function for which you write an end-to-end (E2E) test, start writing
a test for that function and use small cycles of TDD for the helper functions
or dependencies in lower level layers that the new function requires.

Go outside-in (from higher level to lower level) instead of inside-out to:

  * Avoid developing unnecessary code. Since at first it's hard to guess what
    the higher level function will need and you might be tempted to cover
    more cases than the actually required ones.
  * Develop components that are convenient for the upper layer that will use
    them intead of being suited for their lower level dependencies. You will
    be able to imagine the most convenient API you could want from the
    underneath layer.

# Tests

Try to keep tests as simple as possible:
  * Each test should test one feature.
  * Avoid a lot of setup, specially mocks.

If you need to mock often, check the architecture design of your code and
revisit the [S.O.L.I.D.](https://en.wikipedia.org/wiki/SOLID) principles.

For dependencies from other layers try to keep them together in one place,
maybe with a fixture or a helper function,
so that they will be easier to change in the future if
needed. For example, if you need to import the class `Circle` from another
layer during the tests, define a function to instantiate `Circle` instead of
calling it directly from the tests, so that if the functions signature changes,
you'll only have to modify the tests in one place.

## Types of tests

* Unit tests: Use them to test functionality units in your code. Don't test
  dependencies or Python itself (setting constants, basic operators…). You
  don't need to unit test every line of the code, this will make refactoring
  tedious. Instead, test the parts of your code that you really care about,
  not the implementation particularities (you don't have to test helper
  functions for example).
* Integration tests. Check the compatibility between modules or layers at the
  boundaries.
* E2E tests: Test the system from the beginning to end to ensure that the
  functionality that the user wants works as expected. Make as few tests of
  this type as possible, since they are the slowest and will give you the less
  information about where the test originated.

# References

* [“Test-Driven Development with Python” by Harry Percival](https://www.obeythetestinggoat.com/)
* [“Fast Test, Slow Test” by Gary Bernhardt](https://www.youtube.com/watch?v=RAxiiRPHS9k)
