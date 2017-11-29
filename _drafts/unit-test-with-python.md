---
layout: default
title: Unit Testing with Python
---

# Unit Testing with Python

*TODO*
- background
- what is this based on? i.e. which Python version?


## Just before we start...

Let's define and setup a couple of things first before we get started. First, we are going to come up with our own requirements just to that we can use it as a guide to assist with the tutorial. Let's assume we need to build a calculator service to which one of the functions is to allow us to sum two numbers. Secondly, create the files and folders based on the sample structure below:

```bash
my-project/
|
--- calculator.py
|
--- tests/
    |
    --- __init__.py
    |
    --- calculator_test.py

```



## Let's get started

In the previous section, you would have created a few empty Python files.

In calculator.py, it would look something like as a starting point:


```python
class Calculator:

```

Then tests/calculator_test.py would look something like:

```python
import unittest

class CalculatorTest(unittest.TestCase):

```

*TODO*
- what is unittest.TestCase for


You can leave the tests/__init__.py file blank. This is just to let Python know to treat the tests folder as a package. Now, before I show you how the test case would look like, let's consider a few points:
- We'll name our test case as test_should_sum_two_numbers_accurately
- We'll define some test data
- We'll call calculator function to add two numbers - let's call it add_two_numbers
- We'll assert the results

The test case would look something like this:

```python
def test_should_sum_two_numbers_accurately(self):
   # given
   number_one = 3
   number_two = 2
   expected = 5
   calculator = Calculator()

   # when
   actual = calculator.add_two_numbers(number_one, number_two)

   # then
   self.assertEqual(actual, expected)

```

Don't forget to import Calculator class into the test class!

```python
from calculator import Calculator
```

For Calculator, let's create the new method which takes in two parameters and return None for now:

```python
def add_two_numbers(self, first, second):
   return None
```

Running the test (see Executing tests section below on how to execute tests) above will fail as the expected and actual results do not match - which is fine! This is when we'll fix the test by adding a bit of code, run the test and repeat until we are satisfied with the requirement.

A few extra points to note from the above test case:
- Always ensure that your test case starts with "test" - that way unittest will recognise this as a test case
- Consider using a narrative when writing your test case such as "given, when, then" so to help you define:
  - Your test context / test data in the given section
  - What action(s) that need to be carried out in the when section
  - Outcome of the test in the then section


## Executing tests

There are a few different ways you can execute the tests.

To run a suite of tests, you can use unittest's discover. The execution through the command line would look something like:

```bash
python -m unittest discover tests -p "*_test.py" -v
```

The "tests" value instructs unittest to look at this particular folder whilst the "-p" option instructs unittest to run the test(s)r matching certain filename patterns. To enable verbosity output, you just add "-v" into the command.

If you do not want to run a suite of tests within a particular folder, you can execute tests based on a specific module:

```
python -m unittest -v tests.calculator_test
```

There may be situations where you would just run a specific test case, although not something I would recommend. Mainly because, when I made a change to a code, I want to make sure that at my tests are still passing. However, if for whatever reasons you still need to execute just a specific test case, you could execute it like the following:

```bash
python -m unittest tests.calculator_test.CalculatorTest.test_should_sum_two_numbers_accurately
```

## Some other extra stuff

There are times when we need to perform a set of preparations before we execute our test case and / or clean up after we execute out test case - this refers test fixtures.

To prepare a set of actions prior to executing a test case, you define a method called setUp just like the following:

```python
def setUp(self):
   print "Preparing a set of instructions before test case gets executed.."
```

There may be times you need to clean up tasks and the end of every test cases:

```python
def tearDown(self):
   print "Cleaning up after the test case..."

```

