
# Part 2 - Statements
You should already be familiar with common statements like if, while, for, and so on. Unlike an expression a statement does not evaluate to anything. Instead it changes the state of our program, by assigning a variable a new value, by manipulating control flow, handling errors, etc.

As you might expect Python statements often work a little differently from their JavaScript counterparts. The most obvious difference is the syntax though so let's tackle that first.

## Assignment
No don't worry I don't have homework for you. Let's talk about how assignment works in Python.


```python
a = 1
a = 2
print(a)
```

    2
    

Well that's simple enough. No var or let or const. In JS as with most languages initializing a variable and reassigning a variables value uses different syntax. Consider:

```javascript
let a = 1; // variable creation and assignment uses a keyword
a = 2; // reassigning the variable does not
console.log(a);
```

Well in Python we don't use a special keyword. This has some ramifications for scope that we'll cover later.

## If Statements
In JS blocks of code were denoted by braces. This is typical for all the languages that use c-style syntax. Instead Python uses indentation. This is the number one thing that people who don't like Python's syntax don't like. I do like it, it forces you to format your code in a readable way and if you're working with a team you all need to be on the same page about indentation rules. Anyway let's look at an example:


```python
age = 16
if age < 18:
    print("you are not old enough!")
```

    you are not old enough!
    

So a couple things to note here.
1. The conditional does not have parenthises around it. They are required in JS but optional in Python.
2. After the conditional there is a colon, a newline, and an indented block of code with a print function in it. Most IDEs seem to have settled on an indent being four spaces although others use two spaces or a tab or God knows what.

Let's look at a chain of if statements.


```python
age = 16
if age < 18:
    print("You are not old enough.")
elif age < 21:
    print("You are almost old enough.")
else:
    print("You are old enough!")
```

    You are not old enough.
    

Python has this elif keyword. This is short for the "else if" that JS, C, and the usual suspects have. It being its own keyword is convenient for how the parser works, the program that reads your code and transforms it into something the Python interpreter can actually run. This way is arguably less ambigous.

## Handling User Input, the short version
TODO

## While Loops
You'll be familiar with while loops let's while away the hours and write some loops.


```python
count = 10
i = 0
while i < count:
    print(i)
    i += 1
```

    0
    1
    2
    3
    4
    5
    6
    7
    8
    9
    

As I say this should look pretty familiar. When you're writing while loops like this it's very easy to forget the += 1 especially when you write more complicated loops. You don't want to get stuck forever do you?

You also might be wondering about for loops. All in good time.

Let's write a FizzBuzz!


```python
count = 20
i = 0
while i < count:
    message = ""
    if i % 3 == 0:
        message += "Fizz"
    if i % 5 == 0:
        message += "Buzz"
    print(i, message)
    i += 1
```

    0 FizzBuzz
    1 
    2 
    3 Fizz
    4 
    5 Buzz
    6 Fizz
    7 
    8 
    9 Fizz
    10 Buzz
    11 
    12 Fizz
    13 
    14 
    15 FizzBuzz
    16 
    17 
    18 Fizz
    19 
    

#### Nested Loops
I heard you liked while loops so I put a while loop in your while loop so you can while while you while.

This script prints out all the unique combinations of two digits from 1 to 4.


```python
i = 1
while i < 5:
    f = 1
    while f < 5:
        print(i, f)
        f += 1
    i += 1
```

    1 1
    1 2
    1 3
    1 4
    2 1
    2 2
    2 3
    2 4
    3 1
    3 2
    3 3
    3 4
    4 1
    4 2
    4 3
    4 4
    

If you add each pair together which number is most common and why?

You should be aware of the break and continue keywords, a quality bootcamp would certainly at least bring them up. Break is used to prematurely end a loop. Continue skips the rest of the loop and proceeds to the next one at once.

Break in particular is great for escaping otherwise infinite loops. Let's look at an example.


```python
from random import randrange as rr # do as I say, not as I do
tries = 0
while True:
    val = rr(1, 7) + rr(1, 7) + rr(1, 7)
    if val == 18:
        break
    tries += 1
print(tries)
```

    13
    

This script rolls 3d6 over and over again until it gets a maximum roll of 18. Then it prints how many rolls were needed to get that result. You might get lucky or unlucky, after running it a few times the worst result I got was about 400 rolls, the best was 13.

Let's look at a more fun example of a loop where we don't know how many steps it will take. Introducing:

## The Collatz Conjecture
Dun dun dunnnn. It's not too scary I promise. Consider the following given procedure:

- Take a number n
- If it is even divide it by 2
- Otherwise multiply it by 3 and add 1

You can repeat this process as many times as you like. What happens?

Well the Collatz Conjecture says that every number will eventually get to 1. It's a conjecture because mathematitians simply don't know how to prove one way or another. A whole bunch of numbers have been tried and they all eventually make it to one. Let's take this repeated procedure and turn it into a loop.


```python
n = 7
steps = 0
while n > 1:
    if n % 2 == 0:
        n = n // 2
    else:
        n = n * 3 + 1
    print(n)
    steps += 1
print("steps:", steps)
```

    22
    11
    34
    17
    52
    26
    13
    40
    20
    10
    5
    16
    8
    4
    2
    1
    steps: 16
    

Looks pretty tidy doesn't it! Remember the // operator isn't a comment, it enforces integer division. What happens if you use regular division instead?

## Exercise
1. Write a loop that rolls a number of large dice like 10d100 several times. Write a loop that will roll those dice 100 times and print out the highest roll you got.
2. This Collatz Conjecture is neat. Write a loop in a loop. For each number less than 1000 check how many steps it takes to get to one. Print out the number that takes the most steps and how many steps it takes.
3. Call a family member or friend you haven't talked to in a while. Code isn't everything you know!
