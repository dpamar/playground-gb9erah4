# Inc/dec operations

_Reminder : N = [ABCD] with A=B=0 and N = 256*D + C, with cursor on C_

A bit more complex now : increase and decrease value

What does Increase means ? Store N+1 instead of N. In our case : N = D * 256 + C with C < 256. N + 1 = D * 256 + C+1: C+1 is the new C unless C+1 is 256 : then C is 0 and D+1 is the new D
* Set else flag in B
* Increase C
* If C is not null reset else flag
* If else flag is not null (C is null) increase D

_Note: in one case it's increase C, in the other case it's store 0 instead of 255, which is "decrease C" as well_

What does Decrease means ? Store N-1 instead of N. In our case : N = D * 256 + C with C >= 0. N - 1 = D * 256 + C-1: C-1 is the new C unless C is null : then C is 255 and D-1 is the new D
* Set else flag in B
* If C is not null reset else flag
* If else flag is not null (C is null) decrease D
* Decrease C

_Note: in one case it's decrease C, in the other case it's store 255 instead of 0, which is "decrease C" as well_


|Operation|8-bit version|16-bit version|Comments|
|---------|-------------|--------------|--------|
|Increase|+|<+>+[<-]<[->>+<<<]>>]|Increase C, if null increase D|
|Decrease|-|<+>[<-]<[->>-<<<]>>-|If C null decrease D; decrease C|


# Current operation map

|Operation|8-bit version|16-bit version|Comments|
|---------|-------------|--------------|--------|
|Write|.|.|write C (D does not matter)|
|Read|,|,>[-]<|read C and reset D|
|Move left|<|<<<<|Move 4 times|
|Move right|>|>>>>|Move 4 times|
|Increase|+|<+>+[<-]<[->>+<<<]>>]|Increase C, if null increase D|
|Decrease|-|<+>[<-]<[->>-<<<]>>-|If C null decrease D; decrease C|

