# Detecting Deadlock in UNIX
Your task is to design a userspace program that detects and crudely resolves particular types of deadlock on a UNIX system. As we know, deadlock can manifest in a variety of different ways on an operating system, in both the kernel and userland, but for this assignment we will only be concerned with deadlock among userspace processes that are sharing mutually-exclusive file resources. This might sound rather restrictive at first, but as we know, many resources on UNIX machines are in fact represented as files, be they physical or virtual. 

Before you begin, you should have a basic understanding of deadlock and the algorithms for detecting and correcting it.

## Specification

Your program must be written in the C programming language and it must exhibit the following behavior:

0. Print a list of the userspace processes that are actively reading/writing/waiting on any locked file.
1. Check for file-related deadlock amongst the userspace processes that are currently running.
2. If there is no file-related deadlock amongst the userspace processes, print <tt>No deadlock.</tt> to standard out and exit. 
3. If deadlock has been detected, print <tt>Deadlock!</tt>, and then:
4. List each instance of deadlock on a new line and display the process names and file names involved.
5. Kill the process X involved in the most deadlocks and print <tt>Killed X.</tt> to the screen. 
6. Go to 1.

## Hints

This assignment requires you to obtain information about mutually-exclusive (i.e., locked) resources in use by processes that are actively running on your system. You will need to interface with the <tt>/proc</tt> virtual file-system to access this information, which will require a little research on your part. 
Once you have this information, the remainder of the assignment is algorithmic, so you may wish to revisit your notes on algorithms and data-structures. 

If you don't know where to start, see the checkpoints below for guidelines on how to incrementally write your program. Below are some miscellanious things to keep in mind while writing your program.

* Numerical IDs for processes and files are not the same thing as process names and file names.
* To keep the output legible, do not print absolute paths of files, just output their local file names.
* When going from Step 6 to Step 1, new processes might have kicked up, so we need to update the list of the userspace processes that are actively reading/writing/waiting on any locked file (just don't print this list again).

## Grading

If your program does not compile or produce an executable called <tt>ddeadlock</tt> after running <tt>make</tt> on the provided <tt>Makefile</tt>, then you will receive a zero. You will be deducted 1 point per <tt>gcc</tt> warning, so do not throw flags to suppress warnings. Below is a detailed rundown of how you will be evaluated on this assignment.

### Documentation & Style (10 points)

If you are unsure about whether your practices in these two areas are acceptable, then defer to the Indian Hill style guidelines for the C programming language, or some other industrial standard that suits your liking.

If you are concerned about losing points here, then you should meet with your instructor during office hours to be sure things look right.

### I/O Formatting (10 points)

If you do not adhere to the input and output formatting conventions, then you will lose points. You are provided a black-box executable that is a perfect solution, so there should be no ambiguity on the desired input and output.  If you leave debug print statements uncommented in your submission, then you will lose all 10 of these points. Your output should exactly match the output of the black-box, no exceptions.

If you are concerned about losing points here, you may run a <tt>diff</tt> on your output versus the black-box's output to be sure your output exactly matches (whitespace and all).

### Design (10 points)

This assignment is in the C programming language, so we are placing a premium on performance (imagine that this code will be executing on a server with many thousands of running userland processes). You will be docked points if you are too cavalier with system resources, or if parts of your implementation are too convoluted or clunky. If there is any unjustified hard-coding, e.g., placing false limits on the sizes of data-structures for processing input data, then you will lose these 10 points, as your program will crash for large enough input. Finally, you will lose some points here if there are any egregious memory leaks.

If you are concerned about losing points here, then you should meet with your instructor during office hours to see if the part of your solution in question should be redesigned/simplified. 

### Correctness (70 points)

The correctness of your program will account for the majority of your grade. To ensure that you maximize this score, you should develop your code with respect to the milestones listed below.

#### Checkpoint 1 (20 points) 

Step 0, i.e., print to standard out a list of the userspace processes that are actively reading/writing/waiting on any locked file, and then exit.

#### Checkpoint 2 (35 points) 

From Step 0, build a data-structure that represents this information in a way that will be algorithmically useful.

#### Checkpoint 3 (50 points) 

Steps 0-3, i.e., report whether a single deadlock has occurred or not occurred, and then exit.

#### Checkpoint 4 (60 points) 

Steps 0-4, i.e., report whether a single deadlock has occurred or not occurred, print the process names and file names involved in that deadlock, kill any process involved in that deadlock, then repeat.

#### Checkpoint 5 (70 points)

Steps 0-6, i.e., report whether deadlock has occurred or not, and if so, list <i>many</i> ocurrences of deadlock and kill the process involved in the most ocurrences of deadlock, then repeat.

In principle, if you complete all 5 checkpoints, then you will earn full points; however, if any bugs in your code made apparent by the test cases


Finally, as always, you should focus on writing <i>correct</i> code first before you start making your code more efficient. 