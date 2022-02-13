# Detecting Deadlock in UNIX
Your task is to design a userspace program that detects and crudely resolves particular types of deadlock on a UNIX system. As we know, deadlock can manifest in a variety of different ways on an operating system, in both the kernel and user space, but for this assignment we will only be concerned with deadlock among user space processes that are sharing mutually-exclusive <tt>FILE</tt> resources, i.e., files that can be locked.

Before you begin, you should have a basic understanding of deadlock and the algorithms for detecting and correcting it.

## Specification

Your program must be written in the C programming language and it must exhibit the following behavior:

1. Print a list of the user space processes that are actively reading/writing/waiting on any locked file.
2. Check for file-related deadlock amongst the user space processes that are currently running.
3. If there is no file-related deadlock amongst the user space processes, print <tt>No deadlock.</tt> to `stdout` and exit. 
4. If deadlock has been detected, print <tt>Deadlock!</tt>, and then:
5. List each instance of deadlock on a new line and display the process names and file names involved.
6. Kill a process X involved in the most deadlocks and print <tt>Killed X.</tt> to the screen. 
7. Go to 1.

## Hints

This assignment requires you to obtain information about mutually-exclusive (i.e., locked) resources in use by processes that are actively running on your system. You will need to interface with the `/proc` virtual file-system to access this information, which will require a little research on your part. 
Once you have this information, the remainder of the assignment is algorithmic, so you may wish to revisit your notes on algorithms and data-structures. 

If you don't know where to start, see the checkpoints below for guidelines on how to incrementally write your program. Below are some miscellanious things to keep in mind while writing your program.

* Numerical IDs for processes and files are not the same thing as process names and file names.
* To keep the output legible, do not print absolute paths of files, just output their local file names.
* When going from Step 7 to Step 1, new processes might have introduced, so we need to update the list of the userspace processes that are actively reading/writing/waiting on any locked file (just don't print this list again).

## Grading

If your program does not compile or produce an executable called `ddeadlock` after running `make` on the provided `Makefile`, then you will receive at most a 30. You will be deducted 1 point per `gcc` warning, so do not throw flags to suppress warnings. Below is a detailed rundown of how you will be evaluated on this assignment.

### Documentation & Style (10 points)

If you are unsure about whether your practices in these two areas are acceptable, then defer to the Indian Hill style guidelines for the C programming language, or some other industrial standard that suits your liking.

If you are concerned about losing points here, then you should meet with your instructor during office hours to be sure things look right.

### I/O Formatting (10 points)

If you do not adhere to the input and output formatting conventions, then you will lose points. You are provided a black-box executable that is a perfect solution, so there should be no ambiguity on the desired input and output.  If you leave debug print statements uncommented in your submission, then you will lose all 10 of these points. Your output should exactly match the output of the black-box, no exceptions.

If you are concerned about losing points here, you may run a <tt>diff</tt> on your output versus the black-box's output to be sure your output exactly matches (whitespace and all).

### Design (10 points)

This assignment is in the C programming language, so we are placing a premium on performance (imagine that this code will be executing on a server with many hundreds of running user space processes). You will be docked points if you are too cavalier with system resources, or if parts of your implementation are too convoluted or clunky. If there is any unjustified hard-coding, e.g., placing false limits on the sizes of data-structures for processing input data, then you will lose these 10 points, as your program will crash for large enough input. Finally, you will lose some points here if there are any egregious memory leaks.

If you are concerned about losing points here, then you should meet with your instructor during office hours to see if the part of your solution in question should be redesigned/simplified. 

### Correctness (70 points)

The correctness of your program will account for the majority of your grade. To ensure that you maximize this score, you should develop your code with respect to the milestones listed below.

#### Checkpoint 1 (30 points) 

Step 1, i.e., print to `stdout` a list of the user space processes that are actively reading/writing/waiting on any locked file, and then exit.

#### Checkpoint 2 (50 points) 

Next, build a data structure that represents this information in a way that will be algorithmically useful, then perform Steps 1-4, i.e., report whether a single deadlock has occurred or not occurred, and then exit.

#### Checkpoint 3 (60 points) 

Steps 1-5, i.e., report whether a single deadlock has occurred or not occurred, print the process names and file names involved in that deadlock, kill any process involved in that deadlock, then repeat.

#### Checkpoint 4 (70 points)

Steps 1-7, i.e., report whether deadlock has occurred or not, and if so, list <i>many</i> ocurrences of deadlock and kill the process involved in the most ocurrences of deadlock, then repeat.

In principle, if you complete all 5 checkpoints, then you will earn the full 70 points for correctness; however, if any bugs in your code are made apparent by the test cases, then partial credit will be awarded.
