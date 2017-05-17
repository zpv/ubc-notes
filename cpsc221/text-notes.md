# CPSC 221 Textbook Notes
__Steven Zhao__  
_A comprehensive compilation of notes for CPSC 221 2017S1_

##4.5 Single-Linked Lists and Double-Linked Lists
- Vector has the limitation that *insert* and *erase* functions operate in linear $O(n)$ time.
	- Requires a loop to shift elements in the underlying array.
- LinkedList has the ability to add or remove items anywhere in the list in constant $O(1)$ time.
	- Useful when you need to insert and remove elements at arbitrary locations and frequent insertions and removals.
	- No shifts are required
- Each element in a linked list, called a *node*, stores information and a link to the next node in the list. 

### A List Node
- A node is a data structure that contains a data item and one or more *links*.
	- A *link* is a pointer to a node.
- ![UML Diagram](http://cl.ly/0A3E2B1J0Q2s/s.png)
	- A Node contains a data field named *data* of type *Item_Type* and a pointer to a *Node*.
	- The name of the pointer is *next* as shown on the line from the *Node* to itself.
- We can define a *Node* as a C++ **struct**.
	- A **struct** is a data structure that contains data fields and possibly constructors.
	- It is like a class, except that it has no operators.
- The definition of the **struct** *Node* is shown here:  

	```c++
	// Node.h
	#ifndef NODE_H_
	#define NODE_H_
	
	/** A Node is the building block for a single-linked list. */
	struct Node {
		// Data Fields
		/** The data */
		Item_Type data;
		/** The pointer to the next node. */
		Node* next;
		
		// Constructor
		/** Creates a new Node that points to another Node.
			@param data_item The data stored
			@param next_ptr Pointer to the Node that is pointed to by the new Node.
		*/
		Node(const Item_Type& data_item, Node* next_ptr = NULL) : data(data_item), next(next_ptr) {}
	};
	#endif	
	```
	- The constructor initalizes the values of *data* and *next*. We will provide **NULL** as a default value for next.
- ![UML Diagram 2](http://cl.ly/2a213W291a13/s.png)
	- Nodes in a Linked List

### Connecting Nodes
- We can construct the list shown above using the following statements:

	```c++
	Node* tom = new Node("Tom")
	Node* dick = new Node("Dick")
	Node* harry = new Node("Harry");
	Node* sam = new Node("Sam");
	tom->next = dick;
	tom->next = harry;
	harry->next = sam;
	```
	- The statement `tom->next = dick;` stores a pointer (link) to the node with data "Dick" in the data field *next* of the node pointed to by tom.
- Generally, we would have a pointer to the first node in the list and work from there.

	```c++
	Node* head = new Node("Tom");
	head->next = new Node("Dick");
	head->next->next = new Node("Harry");
	head->next->next->next = new Node("Sam");
	```
	- We grew the list by added a new node to the end of the list so far.
	- The node referenced by head was always the first node in the list.
- We can also grow a list by adding nodes to the front of the list.

	```c++
	Node* head = new Node("Sam");
	head = new Node("Harry", head);
	head = new Node("Dick", head);
	head = new Node("Tom", head);
	```
	- Each statement of the form `head = new Node(a_name, head);` creates a new node, who data component is *a_name* and whose next component is the list so far.
	- *head* is reset to point to this new node.
	- This has the effect of adding the new node to the front.

### Inserting a Node in a List
