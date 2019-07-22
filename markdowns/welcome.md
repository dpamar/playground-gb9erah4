# Welcome!

Welcome to this new playground about the BF language. Make sure you already read 
* [Getting started with BrainFuck](https://tech.io/playgrounds/50426/getting-started-with-brainfuck/welcome)
* [BrainFuck part 2 - Working with arrays](https://tech.io/playgrounds/50443/brainfuck-part-2---working-with-arrays/welcome)
* [BrainFuck part 3 - Write a BF interpreter in BF](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 4 - Advanced maths](https://www.codingame.com/playgrounds/50446/brainfuck-part-3---write-a-bf-interpreter-in-bf/welcome)
* [BrainFuck part 5 - Math sequences](https://www.codingame.com/playgrounds/50478/brainfuck-part-5---math-sequences/welcome)

playgrounds if you didn't already !

The goal of this playground is to get rid of a math limition : the "modulo 256" results

What may be annoying using Brainfuck is the size of the cell. You can't (in theory) have integers greater than 255. Of course, this is the case for most of the programming languages, where integers are encoded using either 32 or 64 bits, but the limit is far higher in those cases.

Obviously, the 'cheating' solution would be to use another BF interpreter implementation that supports 16-, 32- or 64-bit integers. But how to use, let's say, 16-bit integers (up to 65,535) using regular Brainfuck? Our only option would be to

* Define a new data structure
* Re-define all the 8 operators using this new data structure
  * What does '+' means ? Add 1. So, how to modify our data that represents an integer N to represents integer 'N+1' instead
  * and same for - , . < > [ ] ...

So, how can we have a new data structure to store 16-bit integers (instead of the actual 8-bit) ?

The naive approach would be to use 2 cells per integer. However, we may need some temporary storage in order to perform the overriden operations like + or -.

Let's defined instead a 4-cell-long structure, ABCD, with
* A = B = 0 (used internally)
* C and D so that N = D * 256 + C

Using this new structure, let's define other operations.
