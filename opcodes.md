# Helix Virtual Machine Opcodes

**0x01** PUSH1 - Pushes 1 : 00-FF to Stack -> `PUSH1 0xFF`
**0x02** PUSH2 - Pushes 2 : 00-FF to Stack -> `PUSH2 0xFFFF`
**0x03** PUSH3 - Pushes 3 : 00-FF to Stack -> `PUSH3 0xFFFFFF`
**0x04** - **0x1F** ...
**0x20** PUSH32 - Pushes 32 : 00-FF to Stack -> `PUSH1 0xFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFFF`

**0x21** DUP1 - Duplications Stack index 1 : Stack Data <1=0x03, 2=0x06> -> `DUP1` = Stack Data <1=0x03, 2=0x03, 3=0x06>
**0x22** DUP2 - Duplications Stack index 2 : Stack Data <1=0x03, 2=0x06> -> `DUP1` = Stack Data <1=0x06, 2=0x03, 3=0x06>
**0x23** DUP3 - Duplications Stack index 3 : Stack Data <1=0x03, 2=0x06, 3=0x07> -> `DUP1` = Stack Data <1=0x07, 2=0x03, 3=0x06, 4=0x07>
**0x24** - **0x30**...
**0x31** DUP16 - Duplications Stack index 3 : Stack Data <1=0x03, ..., 16=0x06> -> `DUP1` = Stack Data <1=0x06, 2=0x03, 17=0x06>

**0x32** STOP - Stop the program
**0x33** ADD - Addition
**0x34** MUL - Multiply
**0x35** SUB - Subtraction
**0x36** DIV - Divide
**0x37** SDIV - Signed Divide
**0x38** MOD - Modulo
**0x39** SMOD - Signed Modulo
**0x3A** EXP - Exponent
**0x3B** LT - Less Than
**0x3C** GT - Greater Than
**0x3D** SLT - Signed Less Than
**0x3E** SGT - Signed Greater Than
**0x3F** ISZERO - Checks if top of stack is = 0. : Stack Data<1=0x00> -> `ISZERO` = Stack Data <1=0x01> ~OTHERWISE~
**0x40** AND - Bitwise AND operation

**0x41** SLOAD - Load in data from storage to defined register
**0x42** SSTORE - Store data from defined register to permanent storage
**0x43** MOV - This will move pointer value to stack -> `PUSH 0x000301 MOV` = move value from pointer 0x0003 from register 01 (r1) to stack
**0x44** CHECK - Will check if a value is present on pointer register (e.g. $0x0001 on 0x01 (r1)) primarly used for checking if program arguments were passed.
**0x45** JUMP - Will jump to defined bytecode -> 
^
|
```
PUSH1 0x04
JUMP
STOP
PUSH2 0xFFA
```
= Will skip the STOP opcode
**0x46** JUMPI - Same as JUMP but checks if top of stack is EQ to zero if so then jump if not then continue

## Token.hvm : An Example
```
PUSH 0x05
CHECK $0x000101
JUMPI
STOP
POP
PUSH 0xA0
CHECK $0x000201
JUMPI
STOP
10 POP
PUSH 0xA5
CHECK $0x000301
JUMPI
STOP
POP
PUSH 0xB9
CHECK $0x000301
JUMPI
STOP
PUSH 0x07
EXT
```