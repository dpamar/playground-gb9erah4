# I/O oeprations

_Reminder : N = [ABCD] with A=B=0 and N = 256*D + C, with cursor on C_

What does Print means ? print ASCII char from code N. If N is greater than 255, we won't get into the complex Unicode stuff : let's just display N modulo 255 (C)

What does Read means ? read ASCII char from input. As it is always less or equal to 255, let's say the C part is read while the D part is equal to 0 (reset)


|Operation|8-bit version|16-bit version|Comments|
|---------|-------------|--------------|--------|
| Write   | .           | .| write C (D does not matter)|
| Read    | ,           | ,>[-]<       | read C and reset D|


