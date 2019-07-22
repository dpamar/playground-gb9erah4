# Loops

_Reminder : N = [ABCD] with A=B=0 and N = 256*D + C, with cursor on C_

The last but not the least : While and Loop

What does While means ? Do if and only if N is not null. N is null if and only if C = D = 0
* Set else flag in B
* If C is not null reset else flag
* If else flag is not null (C is null)
  * Copy D to C (this is just a trick to stay in our 4-cell-long area)
  * If new C (=D) is not null then reset else flag and move back C to D
* Decrease B (1 if and only if C = D = 0, it will be replaced by 0; otherwise it will be 255)
* If B is not null
  * reset B
  * Do the loop stuff

What does Loop means ? Loop to matching While if N is not null. N is null if and only if C = D = 0
* Set else flag in B
* If C is not null reset else flag
* If else flag is not null (C is null)
  * Copy D to C (this is just a trick to stay in our 4-cell-long area)
  * If new C (=D) is not null then reset else flag and move back C to D
* Decrease B (1 if and only if C = D = 0, it will be replaced by 0; otherwise it will be 255)
* If B is not null
  * reset B
  * Do the loop stuff
* Back to C

_Note: the While and Loop focus on cell B. When loop is looping / over, we need to move back to C, our reference cell in this modelisation_


|Operation|8-bit version|16-bit version|Comments|
|---------|-------------|--------------|--------|
|While|[|<+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-[[-]>{loop contents}|Do if and only if C or D is not null|
|Loop|]|<+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-]>|Loop if and only if C or D is not null|

# Current operation map

|Operation|8-bit version|16-bit version|Comments|
|---------|-------------|--------------|--------|
|Write|.|.|write C (D does not matter)|
|Read|,|,>[-]<|read C and reset D|
|Move left|<|<<<<|Move 4 times|
|Move right|>|>>>>|Move 4 times|
|Increase|+|<+>+[<-]<[->>+<<<]>>|Increase C, if null increase D|
|Decrease|-|<+>[<-]<[->>-<<<]>>-|If C null decrease D; decrease C|
|While|[|<+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-[[-]>{loop contents}|Do if and only if C or D is not null|
|Loop|]|<+>[<-]<[>>[-<+>]<[[->+<]<->]<<]>-]>|Loop if and only if C or D is not null|

