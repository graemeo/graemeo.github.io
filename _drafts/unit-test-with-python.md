---
layout: default
title: Unit Testing with Python
---

## Unit Testing with Python


```python
import unittest

class MyFirstTest(unittest.TestCase):

```


Next, let's create a simple test case.


```python
def test_should_concatenate_two_strings(self):
   # given
   first_string = "Hello"
   second_string = "World"
   expected = "Hello World"

   # when
   actual = first_string + " " + second_string

   # then
   self.assertEqual(actual, expected)
```

Note: I like to specify given, when, then in my test cases to guide me in writing my tests such that I know which context of this test is for, what action(s) needs to be carried out and the outcome of this test.

The purpose of the test above is to ensure that, when given two strings, these two strings are concatenated accordingly. The test is probably not that meaningful, but the purpose of this is to give you a basic idea of how a test would look like.

Always ensure that your test case method starts with "test" in the name - that way unittest module will recognise this as a test case.


To run test...

```bash
python -m unittest discover tests -p "*_test.py"
```
