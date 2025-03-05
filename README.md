-- School of Information Technologies and Engineering, ADA University
-- CSCI3510 – Principles of Operating Systems 
-- Spring 2025 – 3/7/2025
-- Assignment 1 by Laman Panakhova 16882

<pre>
                                                  **Readers-Writers Problem with Load Balancing**
</pre>

<pre>
**Instructions**
</pre>


This project implements a solution to the Readers-Writers problem with load balancing. 
The program ensures writer priority over readers and balances the load of readers across multiple file replicas. 
The solution uses threads, synchronization mechanisms (mutexes, condition variables, and semaphores), and logs every read/write operation.


Multiple reader threads spawn at random intervals and read from one of the file replicas.
A single writer thread periodically writes to all file replicas.
The system ensures:
Writers are given priority over readers.
Readers are distributed across file replicas evenly.
The writer locks all file replicas simultaneously and updates their contents.
Features
Fairness: Writers are given priority, and readers must wait for writers to finish their work.
Load Balancing: Readers are distributed evenly across file replicas.
Thread Safety: The program ensures that no two threads access the same file at the same time.
Logging: Logs every read and write operation, including file access details and content.
Randomization: Reader threads start at random intervals, and the writer thread sleeps randomly between write operations.
Requirements
Programming Language: C
Libraries:
pthread.h (for threading)
semaphore.h (for semaphore management)
stdio.h (for logging)
stdlib.h (for random number generation)
unistd.h (for sleep functions)
fcntl.h (for file handling)
string.h (for string manipulation)
time.h (for random seed generation)
Compilation and Running the Program
Prerequisites:
Ensure that you have a C compiler installed (e.g., GCC). The program also uses POSIX threads and semaphores, so your system should support these features.

Steps to Compile and Run:
Clone the repository (if necessary): If you haven't already, clone this repository to your local machine:

bash
Copy
Edit
git clone <repository_url>
cd <repository_directory>
Compile the Program: To compile the program, run the following command in your terminal:

bash
Copy
Edit
gcc -o readers_writers readers_writers.c -lpthread
Run the Program: After compiling, you can run the program using the following command:

bash
Copy
Edit
./readers_writers
Check the Log: The program will create a log.txt file that logs all the operations performed by the reader and writer threads. You can inspect this log to see the system's behavior.

Program Flow
Reader Threads:

A set number of reader threads are created.
Each reader thread attempts to read from one of the file replicas, based on load balancing.
If a writer is active, readers will wait until the writer finishes.
Writer Thread:

The writer thread periodically attempts to write to all three file replicas.
It locks all replicas simultaneously to ensure consistent content across all files.
While the writer is active, no readers are allowed to access the files.
Logging:

Every read and write operation is logged, including the file being accessed, the number of readers, the active writer status, and the file content.
Termination:

The program will run until all reader threads finish and the writer thread completes its operations.
Example Output
In the terminal, you'll see output similar to the following for reader and writer threads:

css
Copy
Edit
Main here. Creating writer thread
Main here. Creating reader thread 0
Reader 0 reading from file1.txt
Main here. Creating reader thread 1
Reader 1 reading from file2.txt
Writer modifying all replicas...
The log file (log.txt) will contain information such as:

yaml
Copy
Edit
Writer active: 1
Readers on file1.txt: 1
Readers on file2.txt: 1
Readers on file3.txt: 0
Content of file1.txt: Updated content by writer
Content of file2.txt: Updated content by writer
Content of file3.txt: Updated content by writer
-----------------------------
Code Structure
readers_writers.c: The main program file containing the implementation.
log.txt: The log file created by the program to track operations.
Makefile (if applicable): For building the project (if you decide to use one).
Design and Synchronization Mechanism
The program uses a combination of:

Mutexes: For mutual exclusion when modifying shared resources like the file replicas and the readers_count array.
Condition Variables: To synchronize reader and writer threads when the writer is active.
Semaphores: To ensure the writer thread operates without interference.
For a more detailed explanation of the design, please refer to the accompanying report.

Known Limitations
The program currently uses random sleep times for simulation purposes, which may not cover all edge cases.
The current implementation logs file content directly, which might not be efficient for very large files.
Future Improvements
Optimizing log handling to avoid repeatedly opening/closing files.
Implementing a more advanced load balancing algorithm for readers.
Graceful thread termination and resource cleanup after execution.
Contact
For questions or feedback, feel free to reach out to the project maintainers.
