# The Ethereum Virtual Machine

In the previous chapter we talked about how *code* written in Vyper
or Solidity is compiled to *bytecode* similar to how *code* in C compiles
to x86 instructions or *code* in Java compiles to execute in the JVM.

The EVM is a stack-based[^2] virtual machine that executes *bytecode*.

Bytecode is essentially a sequential representation of the program's instructions, where each instruction is encoded as a *byte* value.
Generally a Virtual Machine will have it's own set of instruction called **opcodes**, **opcode** are simply
programmatic assignments of high-level code to a number.

<figure>
  <img src="../assets/evm.png" width="600" />
  <figcaption>The EVM illustrated courtesy of <a href="https://takenobu-hs.github.io/downloads/ethereum_evm_illustrated.pdf">EVM Illustrated</a></figcaption>
</figure>

For example to implement a very minimal stack VM in Python that adds two numbers :

```python

# The stack is a FIFO list of objects
stack = []
# Let's define an addition operation and assign to it the number 1.
OPAdd = 0x1
# Let's implement a higher-level function to manipulate the stack
def add(stack):
    # pop two elements from the stack
    a = stack.pop()
    b = stack.pop()
    # calculate their sum
    s = a + b
    # push it down the stack
    stack.append(s)
    return stack

# We can implement higher level functions that interact with the OS and provide for example
# internet access to our VM or access to the hard-drive files through the OS API.
# Or just to print output
def print(stack):
    # pop an element from the stack
    s = stack.pop()
    print(s)
    return stack

# Finally we can implement the execution function that given code and a machine will
# run the code on that VM.
def run(vm,code):
    # for each instruction in the bytecode
    for instr in code:
        # compare it to our known opcodes
        # if there's a match call the high-level
        # function for that opcode.
        if instr == OPAdd:
            vm = add(vm)
    print(vm)
```

The idea behind the EVM is the same although in this case the EVM is sandboxed
and can only interact with the Ethereum state (written in the State Tries) or history (written in the blockchain).

In other words the EVM doesn't interact with the OS so it has no access
to disk, RAM or networking it's essentially self-contained.

[^2]: There are other types of VM's like register-based ones that are similar to your computer.

## EVM Opcodes

EVM Opcodes can be found [here](https://ethervm.io/) or in the [reference](https://github.com/ethereum/go-ethereum/blob/master/core/vm/opcodes.go) `geth` implementation[^1].

[^1]: There are other **evm** implementations such as [pyevm](https://github.com/ethereum/py-evm) which are easier to read.

Each Opcode represents an operation (we only need a limited number to do pretty much anything we can think off) for example :

`OPADD` defines addition of two numbers.

All operations within the EVM operate on a stack.