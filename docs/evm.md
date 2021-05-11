# The Ethereum Virtual Machine

In the previous chapter we talked about how *code* written in Vyper
or Solidity is compiled to *bytecode* similar to how *code* in C compiles
to x86 instructions or *code* in Java compiles to execute in the JVM.

The EVM is a stack-based virtual machine that executes *bytecode* (i.e a set of pre-defined (NUMBER,OPERATION) pair).

The EVM is a sandboxed environment meaning it can only interact with the
Ethereum state (written in the State Tries) or history (written in the blockchain).

In other words the EVM doesn't interact with the OS so it has no access
to disk, RAM or networking it's essentially self-contained.

## EVM Opcodes

EVM Opcodes can be found here or in the [reference] `geth` implementation [source].

Each Opcode represents an operation (we only need a limited number to do pretty much anything we can think off) for example :

`OPADD` defines addition of two numbers.

All operations within the EVM operate on a stack.