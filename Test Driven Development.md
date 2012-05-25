## What is Test Driven Development

The definition of TDD has been argued to death on the internet.
I will define my own version here,
if that matches with your idea, awesome.
If you disagree, that's fine, 
but the point of this article isn't really to argue about names.
So, call it BDD (Behaviour Driven Development) or something else in that case.
What I'm suggesting is not about names, 
but about methods of developing.

So, I define Test Driven Development as the following:

1. failing are written before the code that causes them to pass
2. each test asserts one _expected_ behaviour from the program

Finally 100% code coverage, from this perspective, 
means testing 100% of expected behaviour.
You may not care how your program behaves under certain conditions,
you probably should, 
but if you don't then there is no need to test those conditions.


## Why Use TDD?

One word, Refactoring. 
Refactoring is key to TDD.
If you don't refactor, you're not doing _my_ version of TDD.


## How to Use TDD

TDD can be done well,
and it can be done poorly.
The only way to get better is to practice.
there are many guides, 
but getting your hands dirty is the only real way.

We only suggest two inital things to keep in mind

- get the tests out quickly
- spend your time refactoring

If you can't write tests quickly,
do more drills and tutorials.


## Exploiting TDD with Frequent Changes

Whenever you check out the code, change it.
Leave every repository neater than when you came to it.
In pull-oriented development this is really easy.

1. clone repository
2. create new branch, check in changes
3. push to central repo and open pull request discussing change

Another developer can easily inspect your changes,
and run the tests over your changes.
If the tests pass,
and other developers like your changes,
merge it back into main.

Other developers need only inspect your code for styleistic changes,
the tests assert that the changes to not alter any program logic.


## A Methodic Approach to TDD

Sometimes I just can't get started with TDD.
I don't know where to start.
I believe it is important in any discipline to train yourself in the basics.
The basics are not always the right approach,
but your body should be able to pull of the basics without thinking.
Only then can you really apply more advanced techniques.

### TDD Basics

Every feature is a complete modification of the programs expected behaviour.
All programs contain inputs and outputs, such as the file system, 
a database, a web form, or a keyboard.
In essense, features are defined by their affect on inputs and outputs.

Start by testing your inputs and outputs.
Testing should start at the surface, and proceede deeper over time.

- scaffolding does not need to be tested, it is tested by the compiler.
- discover as much design during refactoring as possible.

