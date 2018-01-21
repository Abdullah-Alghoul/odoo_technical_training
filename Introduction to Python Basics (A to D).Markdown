# A - Installation of Python
## A(1) Installation On Windows operating System
Installation of python on a Windows OS is similar to the installation of any other package.
Download the executable file from https://www.python.org/downloads/.

* **Adding to path**
If you open the command prompt and type python, a less-than-friendly error is thrown stating that no package like that can be found. To fix this however, we should add the location to the system path. Click  on  Control  Panel → System →  Advanced → Environment  Variables.  Click  on  the  variable  named  PATH  in  the System  Variables section, then select Edit and add ;C:\Python27 (please verify that this folder exists.

## A(2) Installation on Linux and Mac
On Mac and GNU/Linux distributions, python should come pre-installed. To check if python is installed on Ubuntu, open the terminal (You can type Ctl + Alt + T). Type this command on the terminal which python.

## Summary  
Python is a language with a simple synthax. It is both easy to read and easy to write. Awareness for python is increasing on a daily basis because of the speed of implementation. It's application cuts accross several operations like data analysis, video gaming, web programming, and even machine learning. It\'s open source nature and portability makes it usable on different platforms. 

# B - Python Basics
Python is a simple to write and understand language. Reading Python feels like reading English. In fact a ... iterated that python feels like writing pseudocodes. Because of some of these qualities of python it recently, in a survey done by Stackoverflow overtook languages like Php as the third most preferred language by developers only trailing the likes of javaScript and PhP. In this section of python baics, we will look at some of the qualoities of the language which includes but are not limited to Extensibility, FLOOS etc.

Python is one of those rare languages which can claim to be both simple and powerful. You will find yourself pleasantly surprised to see how easy it is to concentrate on the solution to the problem rather than the syntax and structure of the language you are programming in.

The official introduction to Python is:  
Python  is  an  easy  to  learn,  powerful  programming  language.  It  has efficient  high-level  data  structures  and  a  simple  but  effective  approach to  object-oriented  programming.  Python’s  elegant  syntax  and  dynamic typing,  together  with  its  interpreted  nature, make it an ideal language for scripting and rapid application development in many areas on most platforms.

## B(1) Features of Python
* **Simple**  
Python is a simple and minimalistic language. Reading a good Python program feels almost like reading English, although very strict English! This pseudo-code nature of Python is one of its greatest strengths. It allows you to concentrate on the solution to the problem rather than the language itself.

* **Easy to Learn** <br>
As  you  will  see,  Python  is  extremely  easy  to  get  started  with.  Python  has  an extraordinarily simple syntax, as already mentioned.

* **Free and Open Source**  
Python is an example of a FLOSS (Free/Libré and Open Source Software). In simple terms, you can freely distribute copies of this software, read its source code, make changes to it, and use pieces of it in new free programs. FLOSS is based on the concept of a community which shares knowledge. This is one of the reasons why Python is so good - it has been created and is constantly improved by a community who just want to see a better Python.

* **High-level Language** <br>
When you write programs in Python, you never need to bother about the low-level details such as managing the memory used by your program, etc.

* **Portable** <br>
Due to its open-source nature, Python has been ported to (i.e. changed to make it work on) many platforms. All your Python programs can work on any of these platforms without requiring any changes at all if you are careful enough to avoid any system-dependent features. You can use Python on GNU/Linux, Windows, FreeBSD, Macintosh, Solaris, OS/2, Amiga, AROS, AS/400, BeOS, OS/390, z/OS, Palm OS, QNX, VMS, Psion, Acorn RISC OS, VxWorks, PlayStation, Sharp Zaurus, Windows CE and PocketPC! You can even use a platform like Kivy to create games for your computer and for iPhone, iPad, and Android.

* **Interpreted** <br>
This requires a bit of explanation. A program written in a compiled language like C or C[]+ is converted from the source language i.e. C or C+ into a language that is spoken by your computer (binary code i.e. 0s and 1s) using a compiler with various flags and options. When you run the program, the linker/loader software copies the program from hard disk to memory and starts running it. Python, on the other hand, does not need compilation to binary. You just run the program directly from the source code. Internally, Python converts the source code into an intermediate form called bytecodes and then translates this into the native language of your computer and then runs it. All this, actually, makes using Python much easier since you don’t have to worry about compiling the program, making sure  that  the  proper  libraries  are  linked  and  loaded, etc. This also makes your Python programs much more portable, since you can just copy your Python program onto another computer and it just works!

* **Object Oriented** <br>
Python supports procedure-oriented programming as well as object-oriented programming. In procedure-oriented languages, the program is built around procedures or functions which are nothing but reusable pieces of programs. In object-oriented languages, the program is built around objects which combine data and functionality. Python has a very powerful but simplistic way of doing OOP, especially when compared to big languages like C++ or Java. 

* **Extensible** <br>
If you need a critical piece of code to run very fast or want to have some piece of algorithm not to be open, you can code that part of your program in C or C\++ and then use it from your Python program.

* **Embeddable** <br>
You can embed Python within your C/C\++ programs to give scripting capabilities for your program’s users.

* **Extensive Libraries** <br>The  Python  Standard  Library  is  huge  indeed.  It  can  help  you  do  various  things involving  regular expressions, documentation generation, unit testing, threading, databases, web browsers, CGI, FTP, email, XML, XML-RPC, HTML, WAV files, cryptography, GUI (graphical user interfaces), and other system-dependent stuff.

## B(2) - First Code -- Hello World!
Enough of all the theories and let's get started with coding. Just like in every other programming course, our aim is to print a message to the console. Open command prompt in Windows or terminal in Mac/Linux and type python (if you get any errors, check the series on how to add python to your system PATH). You should be taken to an environment where you these 3 greater-than symblols (>>>). Type the next command `print("Hello World!")`.

## B(3) - Variables
While building a web app or developing a vidoe game or any other application of sort, we need a way to prompt users for inputs and perform several operations with those input. These input are stored in containers known as variables. Python variables are made of four major types, leaving out the assorted ones list the lists and dictionaries.

* Boolean  
Booleans are list light switches; they have only two states-- on and off --which are True and False.  
Example:
```python
    is_true = True
    is_false = False
    print (type(is_true), type(is_false))
```
The ouput of this code is:  
    `(<type 'bool'>, <type 'bool'>)`

* Integer  
integers are whole numbers without fractional parts. Examples of integers are 1, 2, 4 etc.
Example:
```python
    age = 21
    print(type(age))
```
The code above outputs  
`<type 'int'>`.

* Float  
Floating point numbers are numbers with fractional parts such as 17.90, 8.32, 0.12 etc.  
Example:
```python
    staff_wage = 234.56
    print (type(staff_wage))
```
outputs `<type 'float'>`

* None  
None is a type in Python used to indicate that a variable has no value. This is hardly popular but is still a very important feature of the language. It's can be used to pass a default value as an argument to a function upon which to perform some logic.
Example:  
```python
    name = None
    print(type(name))
```
outputs `<type 'NoneType'>`

## B(4) Adding functionality to our code -- Comments
While the code tells us \'how\', it is the comments that we put in the code that explain why. Commenting is a good attribute of a developer because it expalins to the reader the function of your code even before they are able to absorb the details of the code itself. In practice, this saves the reader (and the reader might even be you).

1. Single-line Comments  
Single-line comments are used to write short notes in the code which do not go beyond a line. Single-line comments are prepended with a (\#) symbol as shown in the code below:

```python
    # I am a single line comment
    print ("Hello world!") # And I am also a single-line comment 
   
```

2. Multi-line comments  
These are used to add comments usually exceeding a line into our code. The comments are enclosed between a pair of three single or double quotation marks on each side.

```python
    '''
    The way python used the multi-line comments is so fascinating
    I cant stop loving it.
    Would you rather come along?
    '''
    def comments():
        """
        Even inside a function block, 
        it works well.
        """
        pass
```

## Summary
Python is indeed an exciting and powerful language. It has the right combination of
performance and features that make writing programs in Python both fun and easy.

# C - Operators and Expressions
Most statements (logical lines) that you write will contain expressions. A simple example of an expression is 2 + 3. An expression can be broken down into operators and operands.

Operators are functionality that do something and can be represented by symbols such as + or by special keywords. Operators require some data to operate on and such data is called operands. In this case, 2 and 3 are the operands. Python has a wide range of operators but we will consider only a few important ones.
Here is a quick overview of the available operators:  
**\+ (plus)**  
Adds two objects  
3 + 5 gives 8. 'a' + 'b' gives 'ab'.

**\- (minus)**  
Gives the subtraction of one number from the other; if the first operand is absent it is assumed to be zero.  
-5.2 gives a negative number and 50 - 24 gives 26.

**\* (multiply)**  
Gives the multiplication of the two numbers or returns the string repeated that many times.  
2 * 3 gives 6. 'la' * 3 gives 'lalala'.

**\*\* (power)**
Returns x to the power of y
3 ** 4 gives 81 (i.e. 3 * 3 * 3 * 3)

**\/ (divide)**
Divide x by y
13 / 3 gives 4. 13.0 / 3 gives 4.333333333333333

**\% (modulo)**
Returns the remainder of the division
13 % 3 gives 1. -25.5 % 2.25 gives 1.5.

**\< (less than)**
Returns whether x is less than y. All comparison operators return 
True or False.
Note the capitalization of these names.  
5 < 3 gives False and 3 < 5 gives True.  

Comparisons can be chained arbitrarily:  
3 < 5 < 7 gives True.

**\> (greater than)**
Returns whether x is greater than y
5 > 3 returns True. If both operands are numbers, they are first converted to a common type. Otherwise, it always returns False.  

**\<= (less than or equal to)**
Returns whether x is less than or equal to y
x = 3; y = 6; x \# y returns True.

**\>= (greater than or equal to)**
Returns whether x is greater than or equal to y
x = 4; y = 3; x >= 3 returns True.

**\== (equal to)**
Compares if the objects are equal
x = 2; y = 2; x == y returns True.
x = 'str'; y = 'stR'; x == y  returns False.
x = 'str'; y = 'str'; x == y  returns True.

**\!= (not equal to)**
Compares if the objects are not equal
x = 2; y = 3; x != y returns True.

**not (boolean NOT)**
If x is True, it returns False. If x is False, it returns True.
x = True; not x returns False.

**and (boolean AND)**
x and y returns False if x is False, else it returns evaluation of y
x = False; y = True; x and y returns False since x is False. In this case, Python will not evaluate y since it knows that the left hand side of the \'and\' expression is False which implies that the whole expression will be False irrespective of the other values. This is called short-circuit evaluation.

**or (boolean OR)**
If x is True, it returns True, else it returns evaluation of y
x = True; y = False; x or y  returns True. Short-circuit evaluation applies here as well.

**Ternary operator**  
Python also has what we call ternary operator. The ternary operation is an if ... else block except that the expression is written on a line.
For instance we want to assign wear to trousers if sex is male otherwise wear is skirt.

```python
    sex  = "Male"
    wear = "Trousers" if sex == "Male" else "Skirt"
    print(wear)
```
The output of the code is `Trousers`. If we change the sex to Female, the output becomes Skirt.

## C(1) -  Operator Precedence
Python has a built in order of executing python expression. however we won't be treating that in this course. To get the official reference material documenting the order of precedence, [follow this link](http://docs.python.org/3/reference/expressions.html#operator-precedence).

## Expressions
We have been using expressions since we started this course. What are expressions? Let's say we have a need to find the area of a rectangle with length 2cm and breadth 4cm. We can go on to perform an operation on the operands using a multiplication (\*) operator and thus assigning the output to a variable called area. This is an expression.
    length = 2  
    breadth = 3  
    area = length * breadth # this is an expression  
We will use expressions throughout our use interaction with python.  

# D - Control Flow
* **If statement**  
We often want to perform an action only after we have checked for a condition, \'If\' statements come in handy in such situations. The basic synthax of the if statement is  
```python
    if <condition>:
        <action_to_perform>
```
Example:  
```python
    name = "Olalekan"
    if name == "Olalekan":
        print ("He's definitely a man!")
```

* **If/Else Statements**
In the last example, we perform an action if our search condition is met, otherwise nothing happens. We oftem want to perform a different action if our test condition is not met. And that is where our If/Else statements play a vital role. The basic structure is:  
```python
    if <condition>:
        <perform_action>
    else:
        <perform_another_action>
```

An example if to a code that prints out if a child is eligible for university based on if s/he is up to 18 years old.

```python
    # This code checks if child is eligible for university
    age = 17
    if age < 18:
        print("You're not eligible for university!")
    else:
        print("Congrats, you can enroll in the university")
```
And this code outputs `You're not eligible for university!`
 
* **If/Elif/Else Statements**  
The If/Elif/Else blocks allow us to check several conditions and perform specific actions based on any of them. We will get the idea better with the use of an example.
```python
    years_of_service = 23
    if years_of_service < 10:
        print("Young employee")
    elif years_of_service < 20:
        print("Intermediate employee")
    else:
        print("Old employee")
```
The code outputs `Old employee`

* **While expression**  
Example:  
```python
    number = 20
    while number > 0:
        print "{num} is greater than 0".format(num=number)
        number -= 1
```
the output of this is:  
```
20 is greater than zero
19 is greater than zero
18 is greater than zero
17 is greater than zero
16 is greater than zero
15 is greater than zero
14 is greater than zero
13 is greater than zero
12 is greater than zero
11 is greater than zero
10 is greater than zero
9 is greater than zero
8 is greater than zero
7 is greater than zero
6 is greater than zero
5 is greater than zero
4 is greater than zero
3 is greater than zero
2 is greater than zero
1 is greater than zero
```
* **For Loop**  
The for loop statement is used to perform iteration over a range of values. The loop repeats till the a termination point is reached. For our example we'll consider the for loop with a range method.
create a python file called for.py and add the following block of code to it.

```python
    for i in range(1, 5):
        print("{}".format(i))
```

The code produces an output of  
```
1
2
3
4
```
Now let's expalain this a little bit. The range() method takes two arguments: the lower bound and the upper bound and generates a list of contiguous values. In our example, the range statement produces a list equivalent to this [1, 2, 3, 4]. So the for statement iterates over the list and prints out each of the items in it.

    + Continue statement
The continue statement is used to skip a loop action for a particular criterium. Let's reconsider our last for loop example. Let\'s skip printing the number three(3). The code looks like this:
```python
    for i in range(1, 5):
    if i == 3:
        continue
    print("{}".format(i))
```
3 is skipped in the output.
```
1
2
4
```  
    + Break statement
The break statement is used to exit a loop prematurely. If in our loop example we want to break out of the loop once we find the number 2, we can introduce a break statement in our code. We tweak the code a little to ensure we print 2 as the last number.
```python
    for i in range(1, 5):
        print("{}".format(i))
    if i == 2:
        break
```

and the output of this is:
```
1
2
```

* Milk 
* Bread 
    + Wholegrain
* Butter
