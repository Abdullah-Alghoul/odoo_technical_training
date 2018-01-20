# (E)
## E(1) Functions (Procedures)
 
These  are reusable pieces of programs. They allows us  to give a name and encapsulate a block of statements*(codes)*,  allowing us to run that block using the specified name anywhere in the program and any number of times. 

The function concept is probably the most important building block of any non-trivial software (in any programming language).

Functions are defined using the __def__ keyword. After this keyword comes an identifier
name for the function, followed by a pair of __parentheses__ which may enclose some names of variables, and by the __final colon__ that ends the line. 
Next follows the block of statements that are part of this function. 

Example:
```python
    def employee():
        """Return profile of an an employee"""
        pass # But this does nothing now.
```
From the block of codes, we define a function called __employee__ using the syntax as explained above. This function takes no *parameters (some people called this arguments, but the real name is parameter)* and hence there are no variables declared in the parentheses.

Parameter is an input variable to functions or procedure definition, that gets an actual value(argument) at execution time. 

They are just input to the function so that we can pass in different values to it and get back corresponding results. Notice that we can call the same function twice which means we do not have to write the same code again.

## E(2) Function Parameters
A function can take zero or as many parametes as needed, which value(s) would be supplied to the function at run time(during execution), the function can then do  something using those values. 

These parameters are just like regular variables except that thier values were defined when we call the function and are already assigned values when the function runs.

Parameters are specified within the pair of parentheses in the function definition, separated by commas. When we call the function, we supply the values in the same way. 

__Note the terminology used - the name of variables given in the function definition are called parameters whereas the values you supply in the function call are called arguments.__

Example:

```python
    # definition of a function maximum.py
    def maximum(a, b):
        """Return the greater number between a and b"""
        if a > b:
            print a, 'is greater than', b
        elif a == b:
            print a, 'and b are equal'
        else:
            print b, 'is greater than', a
            
            
    # Now let us call the our maximum function, by passing value to it directly.
    
    maximum(6, 4) # -> 6 'is greater than', 4
    
    # we can also pass variable as an arguments, which is what we will do almost everytime.
    x = 15
    y = 17
    arguments(x, y) # -> 17, 'is greater than', 15
```
From the above code block, we define a function called maximum that accept  two posotional arguments , i.e parameter a and b . 
We then  find out the greater number using a simple __if..else__ statement and then print the bigger number.

## E(3) Local Variables
When ever  we declared any variable inside a function definition, such variable has no relationship with other variable of the same name declared  outside the function block, i.e. variable names are local to the function. 

This is called the __scope of the variable__. All variables have the
scope of the block they are declared in, starting from the point of definition of the name.

```python
    # employee.py
    
    name = 'babatope ajepe'
    
    def employee(name):
        """Return profile of an an employee"""
        print 'name is', name
        name = 'john doe'
        print 'name is now change to', name
        
        # output
        employee(name) # -> name is babatope ajepe
                       # -> name is now changed to john doe
         print name    # -> babatope ajepe 

```
The first time that we print the value of the name __name__ with the first line in the function’s body/block, Python uses the value of the parameter declared in the main block, above the function definition.

Next, we assign the value 'john doe' to __name__ . The variable name __name__ is local to our function. 
So, when we change the value of __name__ in the function, the __name__ defined in the main block remains unaffected.

The last print statement display the value of __name__ as defined in the main block(global scope), confirming that it is actually unaffected by the local assignment within the previously called function.

## E(4) The global statement

If we want to re-assign or change the value to a __name__ declared at the top level of the program, with our __employee__ function. We need to tell Python that the variable is not local, but it is __global__. 

We can do this using the __global statement__. Practically, It is impossible to re-assign a value to a variable defined outside a function without the use global statement. Using the global statement makes it amply clear that the variable is defined in an outermost block.

Example: 
```python 
 # employee.py

    name = 'babatope ajepe'

    def employee(name):
        """Return profile of an an employee"""
        global name  # referencing the global name outside the employee scope.
        print 'name is', name
        name = 'john doe'
        print 'name is now change to', name

        # output
        employee(name) # -> name is babatope ajepe
                       # -> name is now changed to john doe
         print name    # -> john doe
```

The use of the __global__ statement, tells Python that the variable __name__  is a global variable i.e (outside the local scope) hence, when we re-assign a value to __name__ inside the employee function*(local scope)*, that change the value of __name__ in the global scope.

## E(5) Default Argument Values

For some functions, we may want to make some parameters optional and use default values in case the user does not want to provide values for them. 
This is done with the help of default argument values. we can set default argument values for parameters by appending to the parameter name in the function definition the assignment operator __( = )__ followed by the default value.
__Note that the default argument value should be a constant. More precisely, the default argument value should be immutable.__ 

```python 
    def warning(message, times=1):
        """warn a friend about danger ahead, in number of times."""
        print message * times
        
    shout("Don't play with python, it's very dangerous")    # -> Don't play with python, it's very dangerous
    
    shout("Don't play with python, it's very dangerous", 2) # -> Don't play with python, it's very dangerous  
                                                            # -> Don't play with python, it's very dangerous 
```
The function named __warning__ is used to print a string as many times as specified.  If we don’t supply a value, then by default, the string is printed just once. We achieve this by specifying a default argument value of 1 to the parameter times.

In the first usage of __warning__ , we supply only the string and it prints the string once. In the second usage, we supply both the string and an argument __2__ stating that we want to say the string message two  times.
## E(6) Non keyword and key-worded arguments (\*arg and \**kwargs)

Key worded arguments are \**kwargs are mostly used in function definitions in Odoo. \*args and \**kwargs allow
us  to pass a variable number of arguments to a function. What variable
means here is that we do not know beforehand how many arguments can be passed to our function by the user.
__*args__ is used to send a non-keyworded variable length argument list to the function. 
Example:
```python
    def accumulate(exam_score, *test_scores):
        print "first normal arg:",  exam_score
        for test_score in test_scores:
            print "another arg through *test_scores:", test_score
            
            
accumulate(50, 16, 15)
```
The accumulate function, accept one formal positional arguent and the followed by now-keyword arguments(**arg), this enables us to call the function with an unlimited number of  now-keyword argument.

__\**kwargs__ allows us to pass keyworded variable length of arguments to a function. Let say we want to handle named arguments, we should use \**kwargs in the function. 
Example:
```python 
    def greet_me(**kwargs):
        for key, value in kwargs.items():
            print("{0} = {1}".format(key, value))
            
    greet_me(name="Ajepe babatope") # -> name = Ajepe babatope
```
## E(7) The return statement
The return statement is used to return from a function i.e. break out of the function. We can optionally return a value from the function as well.
```python
    def maximum(a, b):
        """Return the maximum number between a and b."""
        if a > b:
            return a # The execution will break here if a > b
         elif a == b:
             return 'the numbers are equal' # or here if a == b
         else:
             return b # and if b > a it will break here.
         
     print maximum(2, 2) # -> the numbers are equal
```
The __maximum__ function returns the maximum of the parameters, in this case the numbers supplied to the function.
__Note that a return statement without a value is equivalent to return None__ . 
None is a special type in Python that represents nothingness. For example, it is used to indicate that a variable has no value if it has a value of None.

### Summary
We have seen so covered  many aspects of python functions, that woud=ld be needed for Odoo day to day development,  but note that we still haven’t covered all aspects of them.

# F

## Modules
You have seen how we can reuse our code in any program by defining functions once. What if  we wanted to reuse a number of functions in other programs? 

As you might have guessed, the answer is __modules__. There are various methods of writing modules, but the simplest way is to create a __file__ with a __.py__ extension that contains functions and variables.

Another method is to write the modules in the native language in which the Python interpreter itself was written. For example, you can write modules in the C programming language and when compiled, they can be used from your Python code when using the standard Python interpreter.

A module can be imported by another program to make use of its functionality. This is how we can use the Python standard library as well. First, we will see how to use the standard library modules.

```python
    # module.py 
    import sys # This import the module.
    print('The command line arguments are:')
    for i in sys.argv:
        print i
        
    print '\n\nThe PYTHONPATH is', sys.path, '\n'
    
    >> python module.py we are arguments
        # -> The command line arguments are:
        # -> module_using_sys.py
        # -> we
        # -> are
        # -> arguments
    >>  # ['', '/usr/lib/python2.7', '/usr/lib/python2.7/plat-x86_64-linux-gnu', '/usr/lib/python2.7/lib-tk', '/usr/lib/python2.7/lib-old', '/usr/lib/python2.7/lib-dynload', '/home/ajepe/.local/lib/python2.7/site-packages', '/usr/local/lib/python2.7/dist-packages', '/usr/lib/python2.7/dist-packages', '/usr/lib/python2.7/dist-packages/gtk-2.0']
```
First, we import the __sys module__ using the __import__ statement. Basically, this translates to us telling Python that we want to use this module. 
The sys module contains functionality related to the Python interpreter and its environment i.e. the system. When Python executes the import sys statement, it looks for the __sys__ module. In this case, it is one of the built-in modules, and hence Python knows where to find it.

If it was not a compiled module i.e. a module written in Python, then the Python interpreter will search for it in the directories listed in its __sys.path__ variable. 
If the module is found, then the statements in the body of that module are run and the module is made available for you to use. Note that the initialization is done only the first time that we import a module.

## The from ... import statement
If we want to directly import the __argv__ variable into our program (to avoid typing the __sys.__ everytime for it), then we can use the 

```python 
from sys import argv
```
In general, if possible we should try to avoid using this statement and use the import statement instead, by doing that our program will avoid name clashes and will be more readable.

##Creating our own modules
Creating our own modules is a cinch, we have been doing it all along! This is because every __Python program is also a module__. 
We just have to make sure it has a  __.py__ extension. The following example should make it clear.
```python 
    # my_module.py
    def say_hello():
        print 'Hello to the people of the work'
        
    __version__ = '0.0.1'
```
The code above is a sample module. As we can see, there is nothing particularly special about it compared to our usual Python program.  We will next see how to use this module in our other Python programs.
__Note that the module should be placed either in the same directory as the program from which we import it, or in one of the directories listed in *sys.path.*__
```python
    # another_module.py
    import my_module # importing our first module
    # now, let us call say_hello function in my_module
    
    my_module.say_hello() # - > 'Hello to the people of the work'
    print __my_module.__version__ # ->  0.0.1
    
```
Note that we use the same dotted notation to access members of the module.
```python 
    from my_module import say_hello, __version__
    
    say_hello()  # - > 'Hello to the people of the work'
    print 'Version', __version__   # ->  0.0.1
```

### Summary
Just like functions, modules are reusable programs. Packages are another hierarchy to organize modules. The standard library that comes
with Python is an example of such a set of packages and modules. We have seen how to use these modules and create our own modules.