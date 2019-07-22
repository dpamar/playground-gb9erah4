# Be smart

The previous step demonstrated that our model works fine, but is really slow. Actually, we don't always need 16-bit integers : each operation is more expensive on such integers.

So let's reduce their usage as much as possible: and else flag does not have to be a 16-bit 4-cell-long encoded integer !!!

When we read a number (8-bit)
* First cell is the result : this will be a 16-bit integer
* Second cell is the digit read : always less than 256 (actually, between 48 and 57...)
* then we subtract 48, no need to have 16-bit again for this
* then we add 9 times first integer to second : it seems that second needs to be encoded using 4 cells then. But loop counter (9) doesn't.
* and finally we add second to first

Memory will then be
* Final result: 16-bit
* New digit: 16-bit
* Loop counter: 8-bit
* Result copy: 16-bit

One way to proceed is to use standard operation symbols when manupulating 8-bit values, and their names uppercased while manipulating 16-bit ones.

# Code
```
RIGHT
>>,[                   while digit is read
  >++++++[-<-------->] remove 48
  >+++++++++[          do 9 times
    -                  Decrease counter
    LEFT LEFT >>       back to result (cell C)
	WHILE              while not null
	  MINUS            decrease current result
	  RIGHT PLUS       increase current digit
	  > RIGHT PLUS     increase result copy (and goes over counter)
	  LEFT < LEFT      Back to result
	LOOP               loop
	RIGHT > RIGHT      go to copy
	WHILE
	  MINUS LEFT < LEFT
	  PLUS RIGHT > RIGHT
	LOOP               move
	<<<                back to counter
  ]
  <<                   Go to "9 times result  plus current digit"
  WHILE
    MINUS LEFT
	PLUS RIGHT
  LOOP                 Store "10 times result plus current digit into first cell
,]                     read next digit
```

This is the "read integer" code, with some operations on 16 bits and some other on 8 bits. We just have to replace WHILE, MINUS, etc... by the overriden definitions

After that, we can still improve our code by removing things like <>, ><, +- etc... that are (automatically generated) useless instructions.

# Minified version
```
>>>>>>,[>++++++[-<-------->]>+++++++++[-<<<<<<<+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-[[
-]+>[<-]<[->>-<<<]>>->>>+>+[<-]<[->>+<<<]>>>>>>+>+[<-]<[->>+<<<]<<<<<<<<+>[<-]<[>>
[-<+>]<[[->+<]<->]<<]>-]>>>>>>>>>+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-[[-]+>[<-]<[->>-
<<<]>>-<<<<<<<<<<+>+[<-]<[->>+<<<]>>>>>>>>>>+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-]<<]<
<<+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-[[-]+>[<-]<[->>-<<<]>>-<<<<<+>+[<-]<[->>+<<<]>>
>>>+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-]>,]
```

Compared to the initial "read integer" source code where all the operations are converted into 16-bit compliant ones, this minified one is 63% smaller.
