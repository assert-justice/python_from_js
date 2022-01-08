
# Part 1 - Expressions
Welcome to this spiel. This lesson assumes familiarity with JavaScript and is designed to teach python to JS programmers. A lot of attention will be paid to how Python might challenge the assumptions of that audience. Tally-ho!
Expressions and Actual Types

As you should know:

> An expression in a programming language is a syntactic entity that may be evaluated to determine its value.

Below are some examples of expressions that should work as you expect. Note the use of the print function, this is equivalent to JS's console.log.


```python
# Expression examples
print(5 + 5)
print("hello world")
print("hello" + " " + "everyone!")
print(5 ** 3)
```

    10
    hello world
    hello everyone!
    125
    

## Comments and Strings
You start a comment in Python with a # (what I call a pound sign but you whippersnappers call a hashtag). Comments are ignored by the interpreter they are for leaving helpful notes to yourself and others. Writing good comments is more of an art than science and different organizations and teams have different guidelines about them.

```python
# I'm a comment look at me! See how I'm descriptive and updated to reflect code changes? You're welcome.
```

There is a school of thought that says your code should be "self documenting". That is your variable names and function names and so on should be so clear and descriptive comments are unnessesary. This is, not to get to technical, bananas. Yes, your variable names should be clear, your function names should describe the function's purpose. And yes code changes can be made that can then conflict with the old comments. Do it anyway. Even for your own projects. Use full sentences and try to describe the thought process behind a function or file rather than how it literally works line by line. \endrant.

As in JavaScript you can create strings with single quotes or double quotes. Such strings need to be on a single line. Backtics are not used for creating strings, we'll talk about string formatting in a couple lessons.

You can create a multi line string by beginning and ending it with ''' or """. This is actually used to help automatically generate documentation but don't worry about docstrings for now.

```python
# A string literal.
"Ayyy I'm a string literal!"
# Another one
'Using single quotes is also cool.'
# Oh my you're so long...and multi lined.
'''You want a newline?
I got a newline for yous!
I got as many lines as you need ;)'''
```

There are also some special characters you can use for string formatting. A high quality thourough bootcamp will of course go over them.

Suppose you want to put a double quote in a string surrounded by double quotes? Easy you use the escape character \.
```python
# A string literal.
"I'm a \"string\" literal or whatever. No big deal"
```

You can also embed newlines with \n and tabs with \t.


```python
print("Not very readable\n\tAnd yet...\nMagical.")
```

    Not very readable
    	And yet...
    Magical.
    

There are some more special characters but these are the big ones. Just know that me and carriage returns have some beef. Oh and null terminators? Those can wait for C. It's better this way.

## Type Coercion
One of JS's design decisions that was... questionable concerns type coercion. JavaScript is more than willing to convert willy-nilly from numbers to strings to NaNs to who knows what without reporting any errors. Python is much more conservatice.


```python
# An oopsy poopsie
print("5" + 5)
```


    ---------------------------------------------------------------------------

    TypeError                                 Traceback (most recent call last)

    <ipython-input-39-0f3a36204e14> in <module>()
          1 # An oopsy poopsie
    ----> 2 print("5" + 5)
    

    TypeError: must be str, not int


Errors are *a good thing*, we want Python to tell us when we have done something silly. JS is very unwilling to throw errors so it might come off as strict but trust me, it is this way for a reason.

## The Integer Type
Unlike JS, Python has a true integer type. JavaScript uses floating point numbers (64 bit doubles to be exact) to represent all numbers which has some ramifications for doing math. Python by contrast features arbitrarily sized integers. We'll explore what that means shortly.

To get the type of an object in Python is easy, we just use the `type` function!


```python
# Number types
print( type(10) )
print( type(10.0) )
```

    <class 'int'>
    <class 'float'>
    

The only difference between these numbers is the `.0` after the ten that prints as a float. This is how we tell Python what type we want a number to be.

Now for most of the math operators if both inputs are integers the output is an integer. If one or both of them are a float the output is a float. For example


```python
print( 10 + 10.0 )
print( type(10 + 10.0) )
```

    20.0
    <class 'float'>
    

Note that unlike JS, a floating point value of ten is written as `10.0`. The `.0` shows us at a glance that the value of this variable is a float.
This is pretty much the only example of type coercion in Python. There is one operator that behaves a little differently:


```python
print(5 / 2)
print(20 / 2)
```

    2.5
    10.0
    

You'll notice that even though both inputs to the division are integers the output is a float. This is actually a change from Python 2 to Python 3. I won't dwell on the differences between those versions here though.

We have a dedicated operator for integer division.


```python
print(20 // 2)
```

    10
    

Hey! The `.0` is gone! Ok well what if the output isn't a round number?


```python
print( 5 // 2)
```

    2
    

Ok so it rounded `2.5` to `2`. Aren't you supposed to round up in that case? Let's look at more examples. We can convert floats (among other things) to integers with the `int` function.


```python
print( int(9.9) )
```

    9
    

Surely `9.9` should round to `10` right? Well when Python converts a float to an int it doesn't round the number, it *truncates* it. That is to say it throws away the decimal part. It works the same for negative numbers.


```python
print( int(-9.9))
```

    -9
    

Now fun fact this behavior is not standard between different programming languages and even different processors. Emulator developers in particular often are plagued by these nitty gritty details. Fortunately this is a big bag of not your problem for right now. Javascript has a method to do the same operation: `Math.trunc`.

## Arbitrarily Large Integers

Python integers grow as needed to contain arbitrarily large values. A 64 bit unsigned number is a non-negative number stored in, surprise surprise, 64 bits. You can get the maximum size of such a number by raising 2 to the 64th power.


```python
print(2 ** 64)
```

    18446744073709551616
    

That's a big number! But in cryptography we're often working with *256* bit numbers! How high can you count with one of those?


```python
print(2 ** 256)
```

    115792089237316195423570985008687907853269984665640564039457584007913129639936
    

That is a real damn big number. Now JS can handle such numbers, it has the BigInt type for just this purpose. But this is just how Python do right out of the box. As floating point numbers grow bigger they get less accurate. Python integers can be arbitrarily large and perfectly accurate.

## Conditionals and Boolean Logic

As a JS programmer you're familiar with the various boolean operators using the cryptic symbols of !, &&, ||, and so on. Well in Python we just use the English words. Also the true and false boolean values are capitalized as True and False which can be a little hard to remember.


```python
print( False or True ) # true
print( not True) # false
print( not not False or False) # false
print( (not False or False) and True) # true
```

    True
    False
    False
    True
    

## Imports
Python has an extensive standard library and you can of course install more, such as with the pip package manager. Today we'll look at two modules we'll be using a lot in the coming example problems: math and random.

### Math
Python comes with a bunch of math functions in the top level namespace including abs, sum, min, and max. Some math features are consigned to the math module.


```python
import math
print( math.sqrt(10) )
```

    3.1622776601683795
    

Above you can see how we import the math module with the `import` keyword. Then we can use functions from that module with dot notation. In this case we are importing the math module and finding the square root of 10. Suppose you don't like using dot notation, you want to just use the function itself. Easy enough:


```python
from math import sqrt
print( sqrt(10) )
```

    3.1622776601683795
    

Now you can import everything from a module with * but this is not a good idea. You might want to use an alias for an object imported from a module. That's easy enough too.


```python
from math import sqrt as root
print( root(10) )
```

    3.1622776601683795
    

Generally speaking I would encourage you to simply import the module and use dot notation to access methods within it. This will make it very obvious where your functions are coming from, improving readability and making looking up info the docs easier.

To wrap up let's look at a couple common use cases for the random module.


```python
import random
print( random.random() )
```

    0.4928663417241622
    

The above prints out a floating point number between 0 and 1. It has a linear distribution meaning every number in that range is as likely as any other number. Another important function is randrange.


```python
import random
print( random.randrange(1, 7) )
```

    5
    

Here we have written a script that will print out a number between 1 and 6 inclusive. The second argument is 7 because randrange expects a range of values starting from the first argument and ending right before the second. Why did I pick these values? Because they emulate a regular six sided die! So what if you want to roll two of them?

Two six sided dice have a minimum value of 2 and a maximum value of 12 so you might try this:


```python
import random
print( random.randrange(2, 13) )
```

    7
    

That will indeed produce numbers in the right range but they will have the wrong distribution! Not every number between 2 and 12 is as likely as any other. 2 and 12 have only a 1/36 chance of being rolled while a 7 has a whopping 1/6 chance. So in order to emulate the correct distribution we could write the following:


```python
import random
print( random.randrange(1, 7) + random.randrange(1, 7) )
```

    10
    

When we cover loops and functions and things we can write a better dice simulator. But now you know the basics of importing modules!

## Exercises
1. Print out your name, address, age, and whether or not you have a pet with the appropriate datatypes. You could also print out Lady Gaga's information or the president's, I'm not your boss.
2. Think of a real life situation where truncating a number with a decimal point makes more sense than rounding it.
3. Write and print an expression For different dice sizes and combinations. How do you simulate 5 six sided dice (5d6)?  What about 2d10 + 1d4 + 5? How can you make your code less verbose by changing how you import the random module?
