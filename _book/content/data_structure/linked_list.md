# Linked List

The linked list is a list of items, called nodes. Nodes have two parts, value part and link part. Value part is used to stores the data. The value part of the node can be a basic data-type like an integer or it can be some other data-type like a structure. The link part is a pointer, which is used to store addresses of the next element in the list.



The various parts of linked list

1.  **Head** is a pointer that holds the address of the first node in the linked list.
2. **Nodes** Items in the linked list are called nodes.
3. **Value** The data that is stored in each node of the linked list.
4. **Link** Link part of the node is used to store the reference of other node.
   1. next or prev to store address of next or pervious nodes.



##### Types of Linked List

1. [Single Linked List](#single-linked-list)
2. [Double Linked List](#double-linked-list)
3. [Circular Linked List](#circular-linked-list)
4. [Double Circular Linked List](#double-circular-linked-list)



###### Single Linked List

Each node (Except the last node) has a reference to the next node in the linked list. The link portion of node contains the address of the next node. The link portion of the last node contains null.

###### Double Linked List

In a double linked list, there are two pointers in each node. These pointers are called prev and next. The pre pointer of the node will point to the node before it and the next pointer will point to the node next to the given node.

###### Circular Linked List

This type is similar to the singly linked list expect that the last element points to the first node of the list. The link portion of the last node contains the address of the first node.

###### Doubly Circular Linked List



###### Operation

1. Insert element in linked list

   1. Insertion of an element at the start of linked list.
   2. Insertion of an element at the end of linked list.
   3. Insertion of an element at the nth position in linked list.
   4. Insert element in sorted order in linked list.

2. Traversing linked list

3. Search element in a linked list.

4. Delete element in linked list

   1. Delete from head
   2. Delete node from the linked list given its value.
   3. Delete all the occurrence of particular value in linked list.
   4. Delete a single list

5. Reverse a linked list

6. Remove duplicates from the linked list

7. Copy list reversed.

8. Copy the content of given linked list into another linked list

9. Compare two lists.

10. Find length of linked list.

11. Find nth node from beginning.

12. Find nth node from end.

13. **Loop Detect** 

    1. Use some map or hash-table
    2. Slow pointer and fast pointer approach(SPFP).

14. **Loop Detect type**

15. Remove loop (Find loop node, do according if it is circular)

16. Find Intersection

    **Analysis** Find length of both the lists. Find the difference of length of both the lists. Increment the longer list by diff steps, and then increment both the lists and get the intersection point.

    

    