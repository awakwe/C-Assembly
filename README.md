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

Sure, here's a markdown version of the question without revealing the answer:

**Malloc [20 points]**

1. **Given a system with a small amount of memory, which of the following memory allocation algorithms would you use: next-fit or best-fit? Explain the advantages and disadvantages of each of them. [4 points]**

   - **Next-Fit**: The next-fit algorithm starts from the location of the last allocated block and searches for the next block that is large enough to satisfy the request. If it doesn't find a suitable block, it loops back to the beginning of the heap and continues the search.
     - *Advantages*: Can you think of situations where this method would be beneficial?
     - *Disadvantages*: What could be the potential drawbacks of using this method?

   - **Best-Fit**: The best-fit algorithm searches the entire heap to find the smallest block that is large enough to satisfy the request.
     - *Advantages*: What are the benefits of using this method?
     - *Disadvantages*: What could be the potential drawbacks of using this method?

   Considering a system with a small amount of memory, which algorithm would be more suitable and why? Remember to consider factors such as the typical size of allocation requests and the importance of allocation speed versus memory utilization.

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
