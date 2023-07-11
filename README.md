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
