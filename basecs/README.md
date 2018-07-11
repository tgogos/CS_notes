# basecs

by  Vaidehi Joshi [@vaidehijoshi](https://twitter.com/vaidehijoshi)

Click to jump directly to section:
 - [What’s a Linked List, Anyway? [Part 1]](#whats-a-linked-list-anyway-part-1)
 - [What’s a Linked List, Anyway? [Part 2]](#whats-a-linked-list-anyway-part-2)
 - [Stacks and Overflows](#stacks_and_overflows)


<br>
<br>
<br>
<br>
<br>


## What’s a Linked List, Anyway? [Part 1]

One characteristic of linked lists is that they are **linear data structures**, which means that there is a sequence and an order to how they are constructed and traversed. Linear structures, however, are the opposite of non-linear structures. In **non-linear data structures**, items don't have to be arranged in order, which means that we could traverse the data structure *non-sequentially*.

![](imgs/linear_non-linear.jpeg)

The biggest differentiator between arrays and linked lists is the way that they use memory in our machines.

The fundamental difference between arrays and linked lists is that arraysare **static data structures**, whilelinked listsare **dynamic data structures**. A static data structure needs all of its resources to be allocated when the structure is created; this means that even if the structure was to grow or shrink in size and elements were to be added or removed, it still *always needs a given size and amount of memory.* If more elements needed to be added to a static data structure and it didn't have enough memory, you'd need to copy the data of that array, for example, and recreate it with more memory, so that you could add elements to it.

On the other hand, a dynamic data structure can shrink and grow in memory. It doesn't need a set amount of memory to be allocated in order to exist, and its size and shape can change, and the amount of memory it needs can change as well.

![](imgs/memory.jpeg)

> A node only knows about what data it contains, and who its neighbor is.

![](imgs/parts_of_a_linked_list.jpeg)

A ***circular linked list*** is a little odd in that it doesn't end with a node pointing to a null value. Instead, it has a node that acts as the *tail* of the list (rather than the conventional head node), and the node after the tail node is the beginning of the list. This organization structure makes it really easy to add something to the end of the list, because you can begin traversing it at the **tail**node, as the first element and last element point to one another. Circular linked lists can start to get really crazy because we can turn both a singly linked list and a doubly linked list *into* a circular linked list!

![](imgs/types_of_linked_lists.jpeg)









## What’s a Linked List, Anyway? [Part 2]

> There are two major points to consider when thinking about how an algorithm performs: how much time it requires at runtime given how much time and memory it needs.

As far as linked lists go, however, the two types of Big O equations to remember are O(1) and O(n).

![](imgs/big-O-notation.jpeg)

Inserting an element at the beginning of a linked list is particularly nice and efficient because **it takes the same amount of time, no matter how long our list is**, which is to say it has a space time complexity that is *constant*, or **O(1)**.

![](imgs/linked-lists-bigO.jpeg)

A good rule of thumb for remember the characteristics of linked lists is this:

> a linked list is usually efficient when it comes to adding and removing most elements, but can be very slow to search and find a single element.

![](imgs/linked-lists-vs-arrays.jpeg)










## Stacks and Overflows

![](imgs/how_stacks_work.jpeg)
	
![](imgs/stacks_lifo.jpeg)

![](imgs/imp_stacks_arr_vs_llist.jpeg)

![](imgs/push_pop.jpeg)

![](imgs/stacks_in_wild.jpeg)

![](imgs/call_stack.jpeg)
