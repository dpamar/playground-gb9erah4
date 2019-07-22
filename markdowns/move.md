# Move operations

_Reminder : N = [ABCD] with A=B=0 and N = 256*D + C, with cursor on C_

What does Move left means ? Go to previous memory cell. With our 4-cell-long memory integers, it means move 4 times.

What does Move right means ? Go to next memory cell. With our 4-cell-long memory integers, it means move 4 times.

|Operation|8-bit version|16-bit version|Comments|
|---------|-------------|--------------|--------|
|Move left|<|<<<<|Move 4 times|
|Move right|>|>>>>|Move 4 times|


# Current operation map

|Operation|8-bit version|16-bit version|Comments|
|---------|-------------|--------------|--------|
|Write|.|.|write C (D does not matter)|
|Read|,|,>[-]<|read C and reset D|
|Move left|<|<<<<|Move 4 times|
|Move right|>|>>>>|Move 4 times|

