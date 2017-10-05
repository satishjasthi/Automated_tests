# Creating automated testing for python scripts 

Whenever we write functions or classes in a script, in order to test them we manually pass argument's values to functions and test them. However, this can be really daunting when you have a lot of functions and classes defined in our module or script. 

This problem can be easily solved using doctest or unittest modules.

Let's see how to use doctest and unittest with some examples,

Consider the following function 

```python

def fibonacci(n):
  """
  arguments:
  ----------
      n : int
     
  returns:
  -------
      n : int
      
  desc:
  -----
      returns nth value of a fibonacci series
      
  """
  if n == 0:
    return 0
    
  elif n == 1:
    return 1
   
  else:
    return fibonacci(n-1) + fibonacci(n-2)
    
```

In order to test this function either we can use doctest or unittest. Let's see one by one

## doctest:

In case of doctest we test the function for some test cases within the function description as show below

```python

def fibonacci(n):
  """
  arguments:
  ----------
      n : int
     
  returns:
  -------
      n : int
      
  desc:
  -----
      returns nth value of a fibonacci series
  
  >>> fibonacci(0)
  0
  
  >>> fibonacci(1)
  1
  
  >>> fibonacci(7)
  13
  
  """
  if n == 0:
    return 0
    
  elif n == 1:
    return 1
   
  else:
    return fibonacci(n-1) + fibonacci(n-2)
    
def _test():
  import doctest
  doctest.testmod()
  
if __name__ == "__main__":
  _test()
  
```
We can see that fibonacci(n) is being tested on three cases 

- n = 0
- n = 1
- n = 7 

And the new function \_test() is where we import doctest and call .testmod() method to test all functions defined in the script, for the examples defined in their description. In our case it is just one function ie fibonacci(n) and three test cases to test the function.

## unittest:
Now let's see how to use unittest. We will create a new script called Test_fibonacci.py, which is like this

```python

import unittest
from module import fibonacci #module is a script in which we have defined fibonacci function

#Test_fibonacci is a subclass of unittest.TestCase
class Test_fibonacci(unittest.TestCase):
  """
  Test class for all functions within module.py script
  """
  
  def test_fibonacci_general_cases(self):
    """
    Method to test fibonacci function for general cases
    """
    actual = fibonacci(0)
    expected = 0
    self.assertEqual(actual,expected)
    
    actual = fibonacci(1)
    expected = 1
    self.assertEqual(actual,expected)
    
    #we can also do this in single line as 
    self.assertEqual(fibonacci(7),13)
    
if __name__ == "__main__":
  unittest.main(exit = False)

```

When we run this script we get output something like this

```
.
----------------------------------------------------------------------
Ran 1 test in 0.000s

OK
```

Where the single dot represents that one test ie test_fibonacci_general_cases has been run successfully. If we want to add more than one function then just create a new method in the test classs and define the cases for which function needs to be tested.

## Should I use doctest or unittest ?

I prefer to use unittest because some function needs to be tested for several test cases to validate it. Under such conditions, these test cases that are mentioned under description undermines accessibility to actual code of the function as shown below

```python

def function(arg1,arg2....):
  """
  arguments:
  ---------
    arg1:
    arg2:
    .
    .
    .
    
  return:
  -------
    r1:
    r2:
    .
    .
    .
  
  desc:
  -----
  ............................
  ............................
  
  >>> testcase1
  ouput1
  >>> testcase2
  ouput2
  .
  .
  .
  .
  .
  .
  .
  .
  .
  .
  .
  .
  .
  .
  .
  .
  
  """
  #actual code
  .....
  ....
```

We can clearly see that function's actual code is small but there are so many test cases to be tested. Under such cases, unittest is handy where you can just create a new Test_function.py script and define a method to test a function for any number of test cases which doesn't affect the readability of function definition in the source code.

