<!--
author:   U. Anthony Omegbu
email:    anthonyomegbu@gmail.com
version:  0.0.1

tags:     LiaScript, education, OER

logo:     https://your-logo-url.com/logo.jpg

comment:  This document is a simple LiaScript course example.

-->



# C and x86-64 Assembly 
# Exam Study Guide

1. **How many times does function `execv` return if there are no errors?**
   - The `execv` function is like a one-way ticket for a process. It is used to replace the current process image with a new process image. It does not return to the calling process unless there is an error. Therefore, think about how many times it would return if there are no errors.
   - Options:
     - [ ] 0 times
     - [ ] 2 times
     - [ ] 1 time
     - [ ] 3 times

2. **What is the difference between the `%rbx` and the `%ebx` register on an x86-64 machine?**
   - The `%rbx` and `%ebx` are like containers (registers) in the x86-64 architecture. The `%rbx` is a larger container (64-bit register), while the `%ebx` is a smaller container that fits inside the larger one (32-bit register). The `%ebx` register is part of the `%rbx` register. Consider which part of the `%rbx` register the `%ebx` refers to.
   - Options:
     - [ ] `%ebx` refers to only the high order 32 bits of the `%rbx` register
     - [ ] `%ebx` refers to only the low order 32 bits of the `%rbx` register
     - [ ] They are totally different registers
     - [ ] Nothing, they are the same register

3. **What do you NOT expect to find in a Stack Frame?**
   - A stack frame is like a suitcase for a subroutine, containing all the information it needs. This includes saved registers (like clothes), local (automatic) variables (like toiletries), and the return address (like a return ticket). However, one of the options listed is not typically found in a stack frame. Think about what each option represents and which one would not be part of a subroutine's suitcase.
   - Options:
     - [ ] Saved registers
     - [ ] Local (automatic) variables
     - [ ] Function name
     - [ ] Return address


**Malloc [20 points]**

1. **Given a system with a small amount of memory, which of the following memory allocation algorithms would you use: next-fit or best-fit? Explain the advantages and disadvantages of each of them. [4 points]**

   - **Next-Fit**: The next-fit algorithm starts from the location of the last allocated block and searches for the next block that is large enough to satisfy the request. If it doesn't find a suitable block, it loops back to the beginning of the heap and continues the search.
     - *Advantages*: Can you think of situations where this method would be beneficial?
     - *Disadvantages*: What could be the potential drawbacks of using this method?

   - **Best-Fit**: The best-fit algorithm searches the entire heap to find the smallest block that is large enough to satisfy the request.
     - *Advantages*: What are the benefits of using this method?
     - *Disadvantages*: What could be the potential drawbacks of using this method?

   Considering a system with a small amount of memory, which algorithm would be more suitable and why? Remember to consider factors such as the typical size of allocation requests and the importance of allocation speed versus memory utilization.


**2. Consider an allocator implementation with the following characteristics: [16 points]**

- The first-fit free algorithm is used to allocate data.
- All blocks have a header with a size and a pointer to the previous block. The header is 16B (2*8bytes) in size.
- Positive sizes indicate the block is allocated, and negative sizes indicate it is free.
- All freed blocks are immediately coalesced if possible.
- When a block is split, the lower (first) part of the block becomes the allocated part and the upper (second) part becomes the new free block.
- If the heap doesn't have enough space to hold the data, it grows by the minimum amount needed to fit the data. Always successfully.

Given these characteristics, consider the following:

- How would the allocator handle different allocation and deallocation requests?
- What would be the impact on memory fragmentation?
- How would the allocator behave in situations where the heap is nearly full?
- What are the potential advantages and disadvantages of this allocator design?

Remember to consider the specific characteristics of the allocator in your answers.


**Given a heap representation, only the metadata is displayed. For example, the following heap contains an allocated block of size 16, followed by a free block of size 32. The top row contains memory addresses, and the bottom row contains the values stored at those memory addresses.**

```
Address | 0xa000 | 0xa008 | 0xa020 | 0xa028
Value   |   16   | 0x0000 |  -32   | 0xa000
```

**a. (4 points) Assuming an initially empty heap, and given the current state of the heap represented below, which of the malloc sequence was executed?**

- [ ] `p0 = malloc(32); p1 = malloc(32); free(p0);`
- [ ] `p0 = malloc(16); p1 = malloc(32); free(p0); free(p1);`
- [ ] `p0 = malloc(64);`
- [ ] `p0 = malloc(32); p1 = malloc(16); free(p0);`

Consider the state of the heap and the effects of the `malloc` and `free` functions. Which sequence of operations would result in the current heap state?



**b. (4 points) Assuming the heap starts as drawn in the previous question, and given the final state of the heap represented below, which of the malloc sequence was executed?**

```
Address | 0xa000 | 0xa008 | 0xa030 | 0xa038
Value   |   32   | 0x0000 |  -16   | 0xa000
```

- [ ] `p0 = malloc(32); p1 = malloc(16); free(p0);`
- [ ] `p0 = malloc(32); p1 = malloc(16); free(p1);`
- [ ] `p0 = malloc(32);`
- [ ] `p0 = malloc(16);`

Consider the state of the heap and the effects of the `malloc` and `free` functions. Which sequence of operations would result in the current heap state?


**c. (4 points) Assuming the heap starts as drawn above (b), if the following malloc executes, what is the value stored in p1? `p1 = malloc(16);`**

- [ ] `0xa018`
- [ ] `0xa020`
- [ ] `0xa028`
- [ ] `0xa030`
- [ ] `0xa038`
- [ ] `0xa040`
- [ ] `0xa048`

Consider the state of the heap and the effects of the `malloc` function. Where would a block of size 16 be allocated?

**d. (4 points) Assuming the heap starts as drawn above (b), which value can fill the blank to successfully free the first block? `free(____);`**

- [ ] `0xa000`
- [ ] `0xa008`
- [ ] `0xa010`
- [ ] `0xa018`
- [ ] `0xa020`
- [ ] `0xa028`
- [ ] `0xa030`
- [ ] `0xa038`

Consider the state of the heap and the effects of the `free` function. Which address corresponds to the first block that can be freed?



**3. Assembly and Reverse-Engineering [9 points]**

Consider the following assembly dump:

```
0000000000001139 <bloop>:
1139: 55
113a: 48 89 e5
113d: 48 83 ec 10
1141: 48 89 7d f8
1145: 48 83 7d f8 70
114c: 7d 07
1153: 48 05 dd 2e 00 00
1159: 48 89 45 f0
115d: eb b5
1162: b8 00 00 00 00
1167: e8 c0 fe ff ff
116c: 90
116d: c9
116e: c3
```

a. **How many function arguments are defined in the above function bloop? [2 points]**
- [ ] 0
- [ ] 1
- [ ] 2
- [ ] 3

b. **How many local variables (not arguments) are declared in the above function bloop? [2 points]**
- [ ] 0
- [ ] 1
- [ ] 2
- [ ] 3

c. **Which of the following multiplies the value within the rax register by 9? [2 points]**
- [ ] `lea (,rax,9), rax`
- [ ] `lea (rax,rax,8), rax`
- [ ] `lea (rax,rax,9), rax`
- [ ] `lea 9(rax), rax`

d. **If I saw `mov rax, -0x8(%rbp)`, and given char is 1B, short 2B, int 4B, and long 8B, I would say that this local variable is what integer type? [2 points]**
- [ ] int
- [ ] long
- [ ] char
- [ ] short

e. **How many loops does the function above have? [1 point]**
- [ ] 0
- [ ] 1
- [ ] 2
- [ ] 3

Consider the assembly instructions and their effects. What can you infer about the function `bloop` from these instructions?



**4. Reverse Engineering x86-64 to C [16 points]**

Consider the following x86-64 assembly and fill-in the blanks in the C code. Use the following variable-to-register mapping:

- `n` <==> `rdi`
- `result` <==> `eax`
- `i` <==> `rsi`
- `x` <==> `edx`
- `y` <==> `rcx`

You may only use the symbolic variables such as `i`, `x`, and `result` in your C expressions - do not use register names.

```assembly
loop:
    movl $10, %ecx
    movl $0, %eax
    movl $0, %edx
    jmp .L2
.L3:
    leaq (%rax, %rax, 4), %rsi
    movq %rcx, %rax
    leaq (%rcx, %rsi), %rcx
    addq $1, %rdx
.L2:
    leaq (%rdi, %rdi), %rsi
    cmpq %rdx, %rsi
    jg .L3
    ret
```

Fill in the blanks in the following C code to match the assembly code:

```c
long loop(long n) {
    long i = ___;
    long result = ___;
    long x = ___;
    while (___) {
        long y = ___;
        result = ___;
        i++;
    }
    return ___;
}
```

Consider the assembly instructions and their effects. What can you infer about the function `loop` from these instructions?



**5. Consider a program containing this poor-quality code, procedure vulnerable has the following disassembled form on a x86-64 machine: [15 points]**

```c
void vulnerable(char t){
    char password[6];
    char name[4];
    gets(name);
    password[0]='H';
    password[1]='e';
    password[2]='l';
    password[3]='l';
    password[4]='o';
    password[5]=t;
    printf("You cannot know my password %s!\n", name);
}
```

Here is the disassembled form:

```assembly
vulnerable: # @vulnerable
    push %rbp
    mov %rsp, %rbp
    sub $0x10, %rsp
    movb %dil, -1(%rbp) # dil>81sb of rdi
    lea -0xb(%rbp), %rdi
    call gets
    movb $72, -7(%rbp) # H
    movb $101, -6(%rbp) # e
    movb $108, -5(%rbp) # l
    movb $108, -4(%rbp) # l
    movb $111, -3(%rbp) # o
    movb -1(%rbp), %al
    movb %al, -2(%rbp)
    lea -0xb(%rbp), %rsi
    mov $0x400104, %rdi # "You cannot ..
    call printf
    add $0x10, %rsp
    pop %rbp
    retq
```

Given the above C code and its corresponding assembly code, consider the following:

- What are the potential security vulnerabilities in this code?
- How could an attacker potentially exploit these vulnerabilities?
- What changes could be made to the code to mitigate these vulnerabilities?

Remember to consider the specific characteristics of the C code and its corresponding assembly code in your answers.




**For the following questions, recall that:**

- `gets` is the standard C library routine.
- x86-64 machines are little-endian.
- C strings are null-terminated (i.e., terminated by a character with value `0x00`).

**Consider the case where procedure vulnerable is called with argument `t` equal to '1', and we type "Luis" in response to `gets`.**

a. **Which elements of array `password` were overwritten when `gets` is called? [3 points]**
- [ ] None
- [ ] Only `password[0]`
- [ ] `password[0]` and `password[1]`

b. **Which of the following stack values were corrupted? [3 points]**
- [ ] `password[0]`, `password[1]`, and `password[2]`
- [ ] Arguments
- [ ] Arguments and Saved registers
- [ ] Saved registers
- [ ] None of the listed options

Consider the behavior of the `gets` function and the layout of the stack. Which elements of the `password` array and which stack values would be affected by the `gets` call?




c. **What (exactly) was printed by the function when `printf` was executed? [3 points]**

Consider the state of the `name` array and the format string passed to `printf`. What would be the exact output of the `printf` call? Please fill in the blank:

Answer: ________



d. **What would NOT help with preventing code injection attacks? [3 points]**
- [ ] Add a canary to the stack
- [ ] Make the stack larger than it needs to be
- [ ] Make the stack not executable
- [ ] Randomize the memory address of the stack

Consider the various techniques used to prevent code injection attacks. Which of these would not be effective?

e. **Which of the following cases represents a buffer overflow? [3 points]**
- [ ] Writing a string of length 5 to an array of chars of size 6
- [ ] Reading 20B from an array of size 10B
- [ ] Writing 5B of code into a stack buffer with 10B of capacity
- [ ] Executing code in the stack

Consider the definition of a buffer overflow. Which of these scenarios would result in a buffer overflow?



**6. Compiling, linking, loading. For each question, determine at which stage the action happens. [6 points]**

a. **Determine the location of functions in other object files? [2 points]**
- [ ] Compiling
- [ ] Linking
- [ ] Loading
- [ ] Assembling

b. **Place shared libraries in memory? [2 points]**
- [ ] Compiling
- [ ] Loading
- [ ] Linking
- [ ] Assembling

c. **Determine the offset of a stack variable? [2 points]**
- [ ] Compiling
- [ ] Loading
- [ ] Linking
- [ ] Assembling

**7. Answer the questions for the code below. [9 points]**

```c
static int x = 0, y = 5;

int what_is_this(void) {
    x = x + y;
    y = y + 1;
    return y;
}

int main(void) {
    int v = what_is_this();
    printf("%d\n", v);
    return v;
}
```

a. **With respect to the Linker, which of the following is a global symbol? [3 points]**
- [ ] `what_is_this`
- [ ] `y`
- [ ] `x`
- [ ] `v`

b. **With respect to the Linker, which of the following is a local symbol? [3 points]**
- [ ] `v`
- [ ] `what_is_this`
- [ ] `x`
- [ ] `main`

Consider the scope of the variables and functions in the code. Which are global symbols and which are local symbols with respect to the linker?



c. **With respect to the Linker, which of the following is NOT registered as a symbol? [3 points]**
- [ ] `v`
- [ ] `what_is_this`
- [ ] `x`
- [ ] `main`

Consider the scope of the variables and functions in the code. Which of these would not be registered as a symbol by the linker?



**8. For each question, read the code - assume all code is given! [9 points]**

a. **What type of error will the code produce? [3 points]**

```c
int main() {
    int a[4] = {0};
    for (int i=0; i<10000; i++) {
        a[i] = i;
    }
    return 0;
}
```
- [ ] Runtime error
- [ ] Linking error
- [ ] Compilation error
- [ ] Loading error

b. **What type of error will the code produce? [3 points]**

```c
int main() {
    int a[4] = {0};
    for (int i=0; i<4; i++) {
        a[i] = add(a[1], i);
    }
    return 0;
}
```
- [ ] Runtime error
- [ ] Linking error
- [ ] Compilation error
- [ ] Loading error

c. **What type of error will the code produce? [3 points]**

```c
int add(int a, int b);

int main() {
    int a[4] = {0};
    for (int i=0; i<4; i++) {
        a[i] = add(a[1], i);
    }
    return 0;
}
```
- [ ] Runtime error
- [ ] Linking error
- [ ] Compilation error
- [ ] Loading error

Consider the code provided and the types of errors that can occur during different stages of the program's lifecycle. What type of error would each piece of code produce?



**x86-64 calling conventions:**

- Argument registers: `%rdi`, `%rsi`, `%rdx`, `%rcx`, `%r8`, `%r9`
- Preserved registers: `%rbp`, `%rbx`, `%r12`, `%r13`, `%r14`, `%r15`
- Return value: `%rax`, `%rdx`
- Name: `%rax`, `%eax`, `%ax`, `%ah`, `%al`

The `mov` instruction is used to move data between registers, from memory to registers, or from registers to memory. It's a fundamental instruction in x86 assembly language.

Remember that in the x86-64 calling convention, the first six integer or pointer arguments are passed in registers `%rdi`, `%rsi`, `%rdx`, `%rcx`, `%r8`, and `%r9`. Additional arguments are passed on the stack. The return value (if it is an integer or pointer) is passed back to the caller in the `%rax` register. The `%rdx` register is used for certain types of function returns (like returning 128-bit values or using the `div` instruction). The registers `%rbp`, `%rbx`, `%r12`, `%r13`, `%r14`, and `%r15` are callee-saved, meaning that if a function modifies these registers, it must restore their original values before returning.

## Quizzes

Throughout the module, there will be quizzes to test your knowledge on the topics we have covered. These quizzes will help you assess your understanding and identify areas where you may need to review.

> 📢 **Coming Soon!** We're currently working on providing detailed information for various tutoring subjects. Stay tuned for comprehensive explanations and examples. In the meantime, if you have any specific questions or need assistance, feel free to call, text, or email Tony Tutoring ASAP!


## Active Learning Strategies

During the virtual lecture, we will use active learning strategies to engage with the material and deepen our understanding. These strategies may include group discussions, problem-solving activities, and interactive simulations.

> 📢 **Coming Soon!** We're currently working on providing detailed information for various tutoring subjects. Stay tuned for comprehensive explanations and examples. In the meantime, if you have any specific questions or need assistance, feel free to call, text, or email Tony Tutoring ASAP!


## Conclusion

By the end of this module, you should have a strong foundation in Microsoft 365 and be able to apply your knowledge to solve real-world problems.

[preview-lia](https://raw.githubusercontent.com/awakwe/C-Assembly/main/README.md)

[Preview-Lia](https://liascript.github.io/course/?https://raw.githubusercontent.com/awakwe/C-Assembly/main/README.md)
