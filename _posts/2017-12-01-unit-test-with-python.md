---
layout: post
title: To Unit Test or Not to Unit Test
date: 2017-12-01 22:20:00
categories: Python
---

# To Unit Test or Not to Unit Test


For the past 12 months, I have been involved a lot more in writing and maintaining Python scripts. What I have noticed so far, which I don't feel like we are doing enough, is writing unit tests. We may not have written a full blown application using Python, but I don't see why we can't include unit tests for automation scripts written in Python. What I hope to share with you in this post, is the basics of setting up unit tests in Python.

There are a few test frameworks out there which we can use (not something I have experimented yet), however given that Python also ships with unittest module (since Python 2.1 if I'm not mistaken) I thought I should start by playing around with Python's unittest first. Furthermore, the example I have prepared in this post is built on Python 2.7 environment. If you are using an older version of Python (prior to 2.7), you might consider taking a look at unittest2 module (I'll post something about this some time soon).



## Just before we start...

Let's define and setup a couple of things. Firstly, we are going to come up with our own requirements just so that we can use it as a guide to assist with the tutorial. Let's assume we need to build a calculator service to which one of the functions is to allow us to sum two numbers. Secondly, create the files and folders based on the sample structure below:

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

In **calculator.py**, it would look something like this as a starting point:


```python
class Calculator:

```

Then **tests/calculator_test.py** would look something like:

```python
import unittest

class CalculatorTest(unittest.TestCase):

```

Ensure that your test class imports Python's unittest module and the class is subclassed to unittest's TestCase so that you can access the goodness of unittest module.

You can leave the **tests/\_\_init\_\_.py** file blank. This is just to let Python know to treat the tests folder as a package. Now, before I show you how the test case would look like, let's consider a few points:
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

> A few extra points to note from the above test case:
> - Always ensure that your test case starts with "test" - that way unittest will recognise this as a test case
>
> - Consider using a narrative when writing your test case such as "given, when, then" so to help you define:
>   - Your test context / test data in the given section
>   - What action(s) that need to be carried out in the when section
>   - Outcome of the test in the then section
> - assertEqual is just one of the few assertions - refer to [Python's unittest documentation](https://docs.python.org/2/library/unittest.html#unittest.TestCase) for more assertions


## Executing tests

There are a few different ways you can execute the tests.

To run a suite of tests, you can use unittest's discover. The execution through the command line would look something like:

```bash
python -m unittest discover tests -p "*_test.py" -v
```

**tests** refers to the folder to which unittest should start executing the tests from, whilsts **-p** option instructs unittest to execute the test(s) matching certain filename patterns. To enable verbosity output, you just need to add **-v** into the command.

If you do not want to run a suite of tests within a particular folder, you can execute tests based on a specific module:

```
python -m unittest -v tests.calculator_test
```

To execute a specific test case, you could execute it like the following example:


```bash
python -m unittest tests.calculator_test.CalculatorTest.test_should_sum_two_numbers_accurately
```

> Executing just a specifc test case is not something I'm personally fond of; this is mainly because, when I make a change to a code, I wan't to ensure that ALL my tests are still passing. 

## Preparation and / or clean up tasks

There are times when we need to perform a set of preparations before we execute our test case and / or clean up after we execute out test case - this refers test fixtures.

To prepare a set of actions prior to executing a test case, you define a method called **setUp** just like the following:

```python
def setUp(self):
   print "Preparing a set of instructions before test case gets executed.."
```

There may be times you need to clean up tasks and the end of every test cases, this is when you define the **tearDown** method like the following:

```python
def tearDown(self):
   print "Cleaning up after the test case..."

```

## Ignoring tests

If you need to ignore test, refer to the following example:

```python
@unittest.skip("Any comments, perhaps reasoning behind skipping the test?")
def test_ignore_me(self):
   print "This test doesn't do anything"
```

You will need to annotate the test case you are interested in ignoring by including **@unittest.skip("Some comments")**. You can choose to put  meaningful comment as to why you have decided to ignore the test case. 

> Personally, I would strongly discourage to use this feature - mainly because this can lead up to behaviour of ignoring bunch of broken tests without putting effort to fixing it. If a test does not add any value, just simple remove it from your test class. If a test is broken, try to fix it right away rather than ignoring it for later or for someone else to fix.


## To conclude...

What I have included in this post is just a very basic tutorial to get you started. Based on this, you should have enough setup to start building up from then on. If however, you need a complete reference to a working example, you can also check out my sample project here [Python Tests](https://github.com/graemeo/python-tests)
