# HVM: Explained
The HVM is a virtual machine used for running programs on the Helix Network.

## The Stack
The Stack works on a FILO structure. The stack allows function variables
to be easily passed through to a `function` (Refrence "The Function"). 

### Example #1
The FILO Structure
```
PUSH1 0x03
PUSH1 0x04
PUSH1 0x05
```
The stack will be
```
- 0x05 : The Top of the Stack
- 0x04 : The middle of the Stack
- 0x03 : The bottom of the Stack
```

### Data lifetime on the stack
Data stored on the stack will not stay there forever. Once the stack reaches
a size of 1024 items, it will start popping the bottom of the stack to allow for new data
to be added to the stack (Storing data on the stack is much cheaper than on registers).

### Cost of Storage on the Stack
Storing data on the stack is not free, instead it is charge as units of `GAS` (Refrence "The Gas Unit"). Each byte of storage on the stack is equivalent to 1 GAS.

## The Register(s)
Similarly to the Stack the register(s) store(s) data, although instead of storing
data for a simple quick process data on the register(s) stays there for longer.

