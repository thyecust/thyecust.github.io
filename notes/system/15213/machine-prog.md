# 机器编程

## 汇编基础

定义

* Architecture，also ISA. The parts of a processor design that one needs to understand for writing correct machine/assembly code
  * Machine code: bit-level programs that a processor executes
  * Assembly code: A text representation of machine code
* Microarchitecture. Implementation of the architecture.
  * eg, cache sizes and core frequency

Data types

* Integer data of 1,2,4,8 bytes
  * Data values
  * Address
* Floating point data of 4,8,10 bytes
* SIMD vector data of 8,16,32,64 bytes
* Code. Byte sequences encoding series of instructions
* No aggregate types such as arrays or structures

x86-64 Integer Registers

|     |     |     |     |
| --- | --- | --- | --- |
| %rax | %eax | %r8 | %r8d |
| %rbx | %ebx | %r9 | %r9d |
| %rcx | %ecx | %r10 | %r10d |
| %rdx | %edx | %r11 | %r11d |
| %rsi | %esi | %r12 | %r12d |
| %rdi | %edi | %r13 | %r13d |
| %rsp | %esp | %r14 | %r14d |
| %rbp | %ebp | %r15 | %r15d |

* Not part of memory (or cache)

### Moving Data

```assembly
movq Source, Dest
```

Oprand types

* Immediate. `$0x400`, `$-533`
* Register. One of 16 integer registers
