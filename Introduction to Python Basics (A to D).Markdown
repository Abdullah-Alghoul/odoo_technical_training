# A - Installation of Python
## A(1) Installation On Windows operating System
Installation of python on a Windows OS is similar to the installation of any other package.
Download the executable file from [python's official website](https://www.python.org/downloads/).

* **Adding to path**
If you open the command prompt and type python, a less-than-friendly error is thrown stating that no package 
like that can be found. To fix this however, we should add the location to the system path.
click  on  Control  Panel → System →  Advanced → Environment  Variables.  Click  on  the  variable  named  PATH  in  the
System  Variables section, then select Edit and add ;C:\Python27 (please verify that this folder exists.

## A(2) Installation on Linux and Mac
On Mac and GNU/Linux distributions, python should come pre-installed. To check if python is installed on Ubuntu, open the 
terminal (You can type Ctl + Alt + T). Type this command on the terminal which python.

# B - Python Basics
Python is a simple to write and understand language. Reading Python feels like reading English. In fact a ... iterated that python feels like writing pseudocodes. Because of some of these qualities of python it recently, in a survey done by Stackoverflow overtook languages like Php as the third most preferred language by developers only trailing the likes of javaScript and PhP. In this section of python baics, we will look at some of the qualoities of the language which includes but are not limited to Extensibility, FLOOS etc. 

Python is one of those rare languages which can claim to be both simple and powerful. You will find yourself pleasantly surprised to see how easy it is to concentrate on the solution to the problem rather than the syntax and structure of the language you are programming in.

The official introduction to Python is:
Python  is  an  easy  to  learn,  powerful  programming  language.  It  has
efficient  high-level  data  structures  and  a  simple  but  effective  approach
to  object-oriented  programming.  Python’s  elegant  syntax  and  dynamic
typing,  together  with  its  interpreted  nature,  make  it  an  ideal  language
for scripting and rapid application development in many areas on most
platforms.

## B(1) Features of Python
* **Simple** <br>
Python is a simple and minimalistic language. Reading a good Python program feels
almost like reading English, although very strict English! This pseudo-code nature
of Python is one of its greatest strengths. It allows you to concentrate on the solution
to the problem rather than the language itself.

* **Easy to Learn** <br>
As  you  will  see,  Python  is  extremely  easy  to  get  started  with.  Python  has  an
extraordinarily simple syntax, as already mentioned.
Free and Open Source
Python is an example of a 

* **FLOSS**<br>
 (Free/Libré and Open Source Software). In simple terms, you can freely distribute copies of this software, read its source code, make changes to it, and use pieces of it in new free programs. FLOSS is based on the concept of a community which shares knowledge. This is one of the reasons why Python is so good - it has been created and is constantly improved by a community who just want to see a better Python.

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

## B(2) - First Code
Enough of all the theories and let's get started with coding. Just like in every other programming course, our aim is to print a message to the console. Open command prompt in Windows or terminal in Mac/Linux and type python (if you get any errors, check the series on how to add python to your system PATH). You should be taken to an environment where you these 3 greater-than symblols (>>>). Type the next command `print("Hello World!")`.

## B(2) - Variables
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
None is a type in Python used to indicate that a variable has no value. This is hardly popular but is still a very important feature of the language.
Example:  
```python
    name = None
    print(type(name))
```
outputs `<type 'NoneType'>`


## Summary
Python is indeed an exciting and powerful language. It has the right combination of
performance and features that make writing programs in Python both fun and easy.

# C - Operators and Expressions

# D - Control Flow
* **If statement**  
Example:  
```python
    name = "Olalekan"
    if name == "Olalekan":
        print ("He's definitely a man!")
```
