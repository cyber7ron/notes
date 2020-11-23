# Introduction to Assembly

all of this documentation will be for the Intel syntax.

**Compiling**

Assembly code is the code that actually runs on your computer by the processor. For instance take some C code:

```c
#include <stdio.h>

void main(void)
{
    puts("Hello World!");
}
```

That code isn't ran. Thing is that code is compiled into assembly code, which looks like this:

```asm
0000000000001135 <main>:
    1135:       55                      push   rbp
    1136:       48 89 e5                mov    rbp,rsp
    1139:       48 8d 3d c4 0e 00 00    lea    rdi,[rip+0xec4]        # 2004 <_IO_stdin_used+0x4>
    1140:       e8 eb fe ff ff          call   1030 <puts@plt>
    1145:       90                      nop
    1146:       5d                      pop    rbp
    1147:       c3                      ret    
    1148:       0f 1f 84 00 00 00 00    nop    DWORD PTR [rax+rax*1+0x0]
    114f:       00
```

The purpose of languages like C, is that we can program without having to really deal with assembly code. We write code that is handed to a compiler, and the compiler takes that code and generates assembly code.Then the assembly code is what is actually ran on the processor.

with assembly code, there is a lot of different architectures. Different types of processors can run different types of assembly code architectures. The two we are dealing with the most here will be 64 bit, and 32 bit ELF (Executable and Linkable Format). This also called as `x64` and `x86`

**Register**

Registers are essentially places that the processor can store memory. You can think of them as buckets which the processor can store information in. Here is a list of the x64 registers, and what their common use cases are.

```
rbp: Base Pointer, points to the bottom of the current stack frame
rsp: Stack Pointer, points to the top of the current stack frame
rip: Instruction Pointer, points to the instruction to be executed

General Purpose Registers
These can be used for a variety of different things
rax:
rbx:
rcx:
rdx:
rsi:
rdi:
r8:
r9:
r10:
r11:
r12:
r13:
r14:
r15:
```

In `x64` linux arguments to a function are passed via registers.

```
rdi:    First Argument
rsi:    Second Argument
rdx:    Third Argument
rcx:    Fourth Argument
r8:     Fifth Argument
r9:     Sixth Argument
```
with `86` elf architecture, argument are passed on the stack.<br>
also one thing as you may know in C function can return a value.<br>
 In `x64`, this value is passed in the `rax` register. In `x86` this value is passed in the `eax`register.

 Also one thing, there are different sizes for registers. These typical sizes we will be dealing with are 8 bytes, 4 bytes, 2 bytes, and 1. The reason for these different sizes is due to the advancement of technology, we can store more data in a register.   

```
-----------------+---------------+---------------+------------+
| 8 Byte Register | Lower 4 Bytes | Lower 2 Bytes | Lower Byte |
+-----------------+---------------+---------------+------------+
|   rbp           |     ebp       |     bp        |     bpl    |
|   rsp           |     esp       |     sp        |     spl    |
|   rip           |     eip       |               |            |
|   rax           |     eax       |     ax        |     al     |
|   rbx           |     ebx       |     bx        |     bl     |
|   rcx           |     ecx       |     cx        |     cl     |
|   rdx           |     edx       |     dx        |     dl     |
|   rsi           |     esi       |     si        |     sil    |
|   rdi           |     edi       |     di        |     dil    |
|   r8            |     r8d       |     r8w       |     r8b    |
|   r9            |     r9d       |     r9w       |     r9b    |
|   r10           |     r10d      |     r10w      |     r10b   |
|   r11           |     r11d      |     r11w      |     r11b   |
|   r12           |     r12d      |     r12w      |     r12b   |
|   r13           |     r13d      |     r13w      |     r13b   |
|   r14           |     r14d      |     r14w      |     r14b   |
|   r15           |     r15d      |     r15w      |     r15b   |
+-----------------+---------------+---------------+------------+

```
In x64 we will see the 8 byte registers. However in x86 the largest sized registers we can use are the 4 byte registers like ebp, esp, eip etc. Now we can also use smaller registers, than the maximum sized registers for the architecture.

In x64 there is the rax, eax, ax, and al register. The rax register points to the full 8. The eax register is just the lower four bytes of the rax register. The ax register is the last 2 bytes of the rax register. Lastly the al register is the last byte of the rax register.

**words**

word is just two byte data. <br>
dword is four byte of data <br>
qword is eight byte of data.

**stack**

stack is LIFO data structure and its where local variables in the code are stored. we can add or remove value from stack by either pushing them or popping them.

`rbp` : points to the bottom of the stack. <br>
`rsp` : points to the top of the stack.

**Flags**

there is one register that contains flags. A flag is particular bit of this register.

```
00:     Carry Flag
01:     always 1
02:     Parity Flag
03:     always 0
04:     Adjust Flag
05:     always 0
06:     Zero Flag
07:     Sign Flag
08:     Trap Flag
09:     Interruption Flag     
10:     Direction Flag
11:     Overflow Flag
12:     I/O Privilege Field lower bit
13:     I/O Privilege Field higher bit
14:     Nested Task Flag
15:     Resume Flag
```

**Instructions**

*mov* : mov data to one register to another

```asm
mov rax, rdx
```

*dereference* : <br>

If you ever see brackets like [], they are meant to dereference, which deals with pointers. A pointer is a value that points to a particular memory address (it is a memory address). Dereferencing a pointer means to treat a pointer like the value it points to. For instance:

```asm
mov rax, [rdx]

# will move the value pointed to by rdx into the rax register.
```

```
mov [rax], rdx 

# Will move the value of the rdx register into whatever memory is pointed to by the rax register. The actual value of the rax register does not change.
```

*lea* : <br>

The lea instruction calculates the address of the second operand, and moves that address in the first. For instance:

```asm
lea rdi, [rbx+0x10]

# This will move the address rbx+0x10 into the rdi register.
```

*add* : <br>

adds two values together, and stores the sum in the first arguments.

```asm
add rax, rdx

# that will set rax equal to rax + rdx
```

*sub* : subtract the second operand from first and store result in first argument.

```asm
sub rsp, 0x10

# this will set rsp register equal to rsp - 0x10

```

*xor* : this will perform binary operation `xor` on the two arguments its given, and stores the result in the first operation.

```asm
xor rdx, rax
```
That will set the `rdx` register equal to `rdx ^ rax.`

The `and` and `or` operations essentially do the same thing, except with the and or or binary operators.

*push* : it will push the content of a register into stack.

```
push rax
```

*pop* : it will pop the content of the stack

```asm
pop rax
```

*jmp* : The jmp instruction will jump to an instruction address. It is used to redirect code execution. 

```asm
jmp 0x602010
```

*call & ret* : 

This is similar to the jmp instruction. The difference is it will push the values of rbp and rip onto the stack, then jump to whatever address it is given. This is used for calling functions. After the function is finished, a ret instruction is called which uses the pushed values of rbp and rip (saved base and instruction pointers) it can continue execution right where it left off

*jnz / jz*

its similar to jump instruction , the diffrence here is it jump if specific flag is set. `jnz` : jump if not zero. `jz` jump if zero

