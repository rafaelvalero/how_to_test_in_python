
# How to test in python 

Rafael Valero Fernandez
rafaelvalerofernandez@gmail.com
https://sites.google.com/site/rafaelvalerofernandez/

## Motivation

I want to have a little cheatsheet and overview for testing procedures.
I focus in two procedures Doctest and Unittest.

### Why to test?

"Goal of python unit testing is to detect as many bugs and inconsistencies in the infancy of the application development as possible. This is achieved by designing and scripting accurate and quality unit tests that can also serve as detailed documentation for the development process. This ensures that bugs and other problems we catch in the first stages of the development, can be fixed by the development team." From  http://quintagroup.com/cms/python/python-unit-testing.

### Conclusions
1. Test help us to code better, securer and faster.
2. Doctest allows to introduce simple tests in the documentation.

## Doctest

Doctest allows to introduce testing in a very simple way in the very same documentation of the function, for example: 
``` 
    >>> my_function(2,3)
    6
```
where after `>>>` you introduce and example, here `my_function(2,3)` and in the next line the expected output, here `6`. Bellow this example will be workd with more detail.

The basic idea is that **doctest will allow us to introduce simple tests in the documentation**.

Further readings: http://pythontesting.net/framework/doctest/doctest-introduction/ 

**test.py:**


```python
def my_function(a,b):
    """
    This example comes from:
    https://www.youtube.com/watch?v=L8EcFqpX-Lk
    
    >>> my_function(2,3)
    6
    >>> my_function('a',3)
    'aaa'
    """
    return a*b

```

After `my_function` is defined and we introduce the test we want to run in the string line we test using doctest:


```python
import doctest
doctest.run_docstring_examples(my_function, globals(),verbose=True)
# Reference, to use doctest in Jupyter notebooks:
# https://stackoverflow.com/questions/40137950/possible-to-run-python-doctest-on-a-jupyter-cell-function
```

    Finding tests in NoName
    Trying:
        my_function(2,3)
    Expecting:
        6
    ok
    Trying:
        my_function('a',3)
    Expecting:
        'aaa'
    ok


You can also run the code in the shell (as here https://www.youtube.com/watch?v=L8EcFqpX-Lk).
For example:
Function my_function is in a python file named test.py, then you can write in the terminal: `python -m doctest -v test.py`

### References
#### Doctest
Written: 

1.  Sort example and comparison with othen testing procedures: http://docs.python-guide.org/en/latest/writing/tests/
2. doctest documentation: https://docs.python.org/3/library/doctest.html#module-doctest 
3. Comparison and examples between Unittes and Doctest: https://code.tutsplus.com/tutorials/write-professional-unit-tests-in-python--cms-25835

Videos:

1. Sort example from where I borrow example: https://www.youtube.com/watch?v=L8EcFqpX-Lk

## Unittest

The standard workflow is:
1. You define your own class derived from unittest.TestCase.
2. Then you fill it with functions that start with ‘test_’.
3. You run the tests by placing unittest.main() in your file, usually at the bottom.



Further readings: http://pythontesting.net/framework/unittest/unittest-introduction/

For this section I borrow the examples from the first bit of https://www.youtube.com/watch?v=6tNS--WetLI

We need something to test, for example, **calc.py**:

```
# From https://github.com/CoreyMSchafer/code_snippets/blob/master/Python-Unit-Testing/calc.py
# With some modifications.

def add(x, y):
    """Add Function"""
    return x + y


def subtract(x, y):
    """Subtract Function"""
    return x - y


def multiply(x, y):
    """Multiply Function"""
    return x * y


def divide(x, y):
    """Divide Function"""
    if y == 0:
        raise ValueError('Can not divide by zero!')
    #return float(x) / float(y)
    return x / y # That will give us a failure in the test: self.assertEqual(calc.divide(5, 2), 2.5)
```

And we will test the previous logits by using some tests which are in file: **test_calc.py**

```
# from https://github.com/CoreyMSchafer/code_snippets/blob/master/Python-Unit-Testing/test_calc.py
# With some modifications.

import unittest
import calc


class TestCalc(unittest.TestCase):

    def test_add(self):
        self.assertEqual(calc.add(10, 5), 15)
        self.assertEqual(calc.add(-1, 1), 0)
        self.assertEqual(calc.add(-1, -1), -2)

    def test_subtract(self):
        self.assertEqual(calc.subtract(10, 5), 5)
        self.assertEqual(calc.subtract(-1, 1), -2)
        self.assertEqual(calc.subtract(-1, -1), 0)

    def test_multiply(self):
        self.assertEqual(calc.multiply(10, 5), 50)
        self.assertEqual(calc.multiply(-1, 1), -1)
        self.assertEqual(calc.multiply(-1, -1), 1)

    def test_divide(self):
        self.assertEqual(calc.divide(10, 5), 2)
        self.assertEqual(calc.divide(-1, 1), -1)
        self.assertEqual(calc.divide(-1, -1), 1)
        self.assertEqual(calc.divide(5, 2), 2.5)

        with self.assertRaises(ValueError):
            calc.divide(10, 0)


if __name__ == '__main__':
    # When run this module directly then run the code within the conditional
    unittest.main()
    # This run all the tests
    # So we can run this code from the editor too.

```

Which results is (after running it in the command line:  `python test_calc.py`
```
....
----------------------------------------------------------------------
Ran 4 tests in 0.000s
```



```python

```

### References
#### Unittest
Written: 

1. Sort example and comparison with othen testing procedures: http://docs.python-guide.org/en/latest/writing/tests/
3. Comparison and examples between Unittes and Doctest: https://code.tutsplus.com/tutorials/write-professional-unit-tests-in-python--cms-25835

Videos:

1. From where I borrow example: https://www.youtube.com/watch?v=6tNS--WetLI


```python

```


```python

```
