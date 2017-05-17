# CPSC 221 Class Notes
__Steven Zhao__  
_A comprehensive compilation of notes for CPSC 221 2017S1_

## Lecture 1
### What is a Data Structure?
* Examples: list, queue, heap, stack, tree, array, graph
* Collections that can hold/store/retrieve/manipulate data

### Observation
* All programs manipulate data
	* Programs process, store, display, and gather data
	* Data can be information, numbers, images, sound, etc.
* The programmer must decide how to store and manipulate data
* This choice influences the program in many ways.
	* Execution speed
	* Memory requirements
	* Maintenance (debugging, extending, etc.)

### Analysis Example: Fibonacci Numbers
- A Fibonacci sequence is one where the first two numbers 1 and each succeeding number is the sum of the previous two nubmers.
- Recursive Fibonacci in C++ code:

	```c++
	int fib(int n) {
		if (n <= 2)
			return 1;
		return fib(n-1) + fib(n-2);
	}
	```
	- $A_n =$ # of additions performed by fib(n) $A_n \geq fib(n)$
- Iterative Fibonnaci
	- Idea: Use an array

	```c++
	int fib(int n) {
		int F[n+1];
		
		F[0]=0; F[1]=1; F[2]=1;
		for(int i=3; i <= n; ++i) {
			F[i] = F[i-1] + F[i-2];
		}
		return F[n];
	}
	```
- Fibonacci by Formula
	- Idea: Use a formula $$fib_n = \frac{\phi^n-(-\phi)^{-n}}{\sqrt{5}}$$ where $\phi = (1 + \sqrt{5})/2 \approx1.61803$

	```c++
	#include <cmath>
	int fib(int n) {
		double phi = (1 + sqrt(5))/2;
		return (pow(phi, n) - pow(-phi, -n)/sqrt(5);
	}
	```
	- It is in O(log n) as pow(n) takes about logn multiplications
	- Sadly, it is impossible to represent $\sqrt{5}$ exactly on a digital computer.

### Abstract Data Type
- Mathematical description (what we are storing) of an object and the set of operations on the object.
- Example: **Dictionary ADT**
	- Stores pairs of strings: (word, definition)
	- Operations
		- Insert(word, definition)
		- Delete(word)
		- Find(word)

### Array ADT
- Store things like integers, (pointers to) strings, etc.
- Operations:
	- Initialize an empty array that can hold n things.
	- Access (read or write) the ith thing in the array.
- Why Arrays?
	- Computer memory is an array.
		- Read: CPU provides address i, memory unit returns the data stored at i.
		- Write: CPU provides address i and data d, memory unit stores data d at i.
		- Simple and fast
		- Used in almost every program.
		- Used to implement other data structures
- Array Limitations
	- We need to know the size of the whole array when the array is created
		- **Fix:** Resizeable arrays.  
		If the array fills up, allocate a new, bigger array and copying old contents to the new array. Then, delete the old array.
	- Indices are integers 0, 1, 2,...
		- **Fix:** Hashing. This will give us more flexibility. (more later)
		- i.e. associative arrays: JavaScript, Python  
		A["dictionary"] = "..."
- Array ADT Implementation
	- create_array(size) and returns address
	- A = address of the 0th elements
	- A[3] = A  3 * size(element) which is the address of A[3]
	- **double array:**

	```c++
	double A[100];
	A + 3 // pointer arithmetic
	A[3] = *(A+3) // dereferencing
	```
	- Arrays in C++
		- To create: int A[100]
			- g++ will not initialize.
			- vc++ initializes to 0's
		- To access:
		
		```c++
		for (int i=0; i < 100; i++)
		A[i] = (i+1) * A[i-1];
		```
		
### Data Structures as Algorithms; Abstract Data Types
#### Algorithm
- An algorithm is a high-level, language dependent description of a step-by-step process for solving a problem.
- There may be multiple algorithms for solving a problem, and some may be more efficient than others.

#### Data Structure
- A data structure provides a way of storing and organization data so that it can be manipulated by an ADT.
- An ADT describes *what* is stored, and it defines the *interface* (set of operations)
- An ADT is implemented by a data structure which specifies *how* the data is stored, and it provides *algorithms*

> data structures specifies how; implements operators for ADT.

### Why So Many Data Structures?
#### Ideal Data Structure
- Fast, elegant, memory efficient

#### Trade-offs
- Time vs. space
- Performance vs. elegance
- Generality vs. simplicity
- One operation's performance vs another's

#### Example: Data Structures for a dictionary ADT
- List, Skip list, Binary search tree, AVL tree, Splay tree, B-tree, Red-Black tree, Hash table

### Code Implemntation for a Dictionary
#### Theory
- An abstract base class (interface) describes the ADT.
- Descedents implement the data structure for the ADT.
- Data structures can change without affecting the client code.

#### Practice
- Different implementations sometimes suggest different interfaces (generality vs simplicity)
- The performance of a data structure may influence the form of the client code (time vs. space, one operation vs. another)



### ADT Presentation Algorithm
1. Present an ADT
2. Motivate it using some applications
3. Repeat  
3.1. Develop a data structure for the ADT.  
3.2. Analyze its properties:
	- Efficiency
	- Correctness
	- Limitations
	- Ease of programming
4. Contrast the data structure's strengths and weaknesses; understand when to use each one 

### Queue ADT
#### Queue operations
- create
- destroy
- enqueue
- dequeue
- is_empty

#### Queue property
If `x` is enqueued before `y` is enqueued, then `x` will be dequeued before `y` is dequeued.

> FIFO: First in First Out

### Applications of a Queue (Q)
- Hodling jobs for a printer
- Storing packets on network routers
- Holding memory "freelists"
- Making wait lists fair
- Performing a breadth-first search (BFS)

> Breadth-first search (BFS) is an algorithm for traversing or searching tree or graph data structures. It starts at the tree root (or some arbitrary node of a graph, sometimes referred to as a 'search key'[1]) and explores the neighbor nodes first, before moving to the next level neighbors.

### Abstract Q Example
![Ab](http://cl.ly/1X1a0B1M2E46/s.png)

### Circular Array Q Data Structure
![Circular Array Q Data Structure](http://cl.ly/0n3m460f1i0Q/s.png)