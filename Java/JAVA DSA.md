

# [Collection Framework](https://youtu.be/rzA7UJ-hQn4)



---
# DSA

TODO:
+ make notes from gateway
+ searching and shorting

---
**Note :**
+ Add at end, remove at end = LIFO (Stack)
+ Add at end, remove at front = FIFO (Queue)

# Dynamic Array

+ Dynamic array in java i.e. ArrayList, Vector etc
+ ArrayList takes object. That's why we use wrapper classes like Integer, Boolean
+ It is a collection.

## ArrayList

```java
import java.util.ArrayList;

public class ArrayListUse{
	public static void main(String[] args){
		ArrayList<Integer> a1=new ArrayList<Interger>();
		
		a1.add(10); //add to the last
		a1.add(30);
		a1.add(40);
		
		a1.add(0,20); // add at specified location
		
		System.out.println(a1.size()); //arraylist size
		
		System.out.println(a1); //printing arraylist
		
		System.out.println(a1.get(0)); //get element at index 0
		
		//printing the list
		for (int i=0;i<a1.size();i++){
			System.out.println(a1.get(i));
		}
		
		a1.remove(0); //remove index from specific element
		
		a1.set(1,50); //set replaces the element
		
		//print all element using for each
		for(int element: a1){
			System.out.println(element+" ");
		}
	}
}
```



---
# LinkedList

## Singly Linked list
i.e. generic type singly linked list
```java
public class Node<T>{
	private T data;
	private Node<T> next;
	
	public Node(T data){
		this.data=data;
		this.next=null;
	}
	
	public T getData(){
		return this.data;
	}
}
```

```java
public class NodeUse{
	public static void main(String[] args){
		Node<Integer> n1=new Node<>(10);
		Node<Integer> n2=new Node<>(20);
		Node<Integer> n3=new Node<>(30);
		
		n1.next=n2; //n1.next is used to access the field(or instance variable) of Node object
		n2.next=n3;
		
		System.out.println(n1.getData()); //to print n1 data
		
		//to print whole list
		Node<Integer> head=n1;
		while(head!=null){
			System.out.print(head.getData()+"->");
			head=head.next;
		}
	}
}
```


**Generic type Node for Linked List Implementation**
```java
public class Node<T> {
	private T data;
	private Node<T> next;
	
	public Node(T data){
		this.data=data;
		this.next=null;
	}
	public T getData(){
		return this.data;
	}
	public Node<T> getNext(){
		return this.next;
	}
	public void setData(T data){
		this.data=data;
	}
	public void setNext(Node<T> next){
		this.next=next;
	}
}
```

**`TakeInput`** Time Complexity O(n^2)
```java
import java.util.Scanner;
public class LinkedList{
	private static Node<Integer> takeInput(){
		Node<Integer> head=null;
		Scanner s=new Scanner(System.in);
		int data=s.nextInt();
		
		while(data==-1){
			Node<Integer> newNode=new Node<>(data);
			if(head==null){
				head=newNode;
			}
			else{
				Node<Integer> temp=head;
				while(temp.getNext()!=null){
					temp=temp.getNext();
				}
				temp.setNext(newNode);
			}
			data.s.nextInt();
		}
		s.close();
		return head;
	}
	
	private static void printLL(Node<Integer> head){
		Node<Integer> temp=head;
		while(temp!=null){
			System.out.print(temp.getData()+"->");
			temp=temp.getNext();
		}
		System.out.println();
	}
	
	public static void main(String[] args){
		Node<Integer> head=takeInput();
		printLL(head);
	}
}
```

# Linked List Operations in Java

## Linked List implementation

**`TakeInput`** Time Complexity : O(n)
```java
import java.util.Scanner;

public class LinkedListBetter{
    //repetedly take input and create linked list
    public static Node<Integer> takeInput(Scanner s){
        int data=s.nextInt();
        Node<Integer> head=null,tail=null;
		
        while (data!=-1) {
            Node<Integer> newNode=new Node<Integer>(data);
            if(head==null){
                head=newNode;
                tail=newNode;
            }else{
                tail.setNext(newNode);
                tail=newNode;
            }
            data=s.nextInt();
        }
        return head;
    }
    // insert at given position
    public static Node<Integer> insert(Node<Integer> head,int pos,int data){
        Node<Integer> temp=head;
        Node<Integer> newNode=new Node<>(data);
        int count=0;
		
        if(pos==0){
            newNode.setNext(temp);
            head=newNode;
            return head;
        }else{
            while (count!=pos && temp!=null) { //here temp!=null bcz we also want to insert at last position
                temp=temp.getNext();
                count++;
            }
            if(temp!=null){ // Insert after the found node
                Node<Integer> rightLL=temp.getNext();
                temp.setNext(newNode);
                newNode.setNext(rightLL);
            }else{
                System.out.println("position out of bound");
            }
        }
        return head;
    }
	
    //length of linked list
    private static int length(Node<Integer> head){
        Node<Integer> temp=head;
        int count=0;
        while(temp!=null){
            temp=temp.getNext();
            count++;
        }
        return count;
    }
	
    // delete node from the given position in linked list
    private static Node<Integer> delete(Node<Integer> head,int pos){
        Node<Integer> temp=head,prev=null;
        int count=0;
        if(head==null){
            System.out.println("List is empty");
            return head;
        }
        else if(pos==0){
            head=temp.getNext();
            return head;
        }else{
            while (count!=pos && temp!=null) {
                prev=temp;
                temp=temp.getNext();
                count++;
            }
            if(temp!=null && temp.getNext()!=null){ 
                prev.setNext(temp.getNext());
            }else if(temp.getNext()==null){
                prev.setNext(null);
            }
            else{
                System.out.println("positon is out of bound");
            }
        }
        return head;
    }
	
    // print whole linked list
    public static void printLL(Node<Integer> head){
        Node<Integer> temp=head;
        while (temp!=null) {
            System.out.print(temp.getData()+"->");
            temp=temp.getNext();
        }
        System.out.println();
    }
	
    // print data of given position in linked list
    private static void printAt(Node<Integer> head,int pos){
        int count=0;
        System.out.println("Enter the position to print value : ");
        Node<Integer> temp=head;
        while(count!=pos && temp!=null){
            temp=temp.getNext();
            count++;
        }
        if(count==pos && temp!=null){
            System.out.println("Data at position " + pos + ": " + temp.getData());
        }else{
            System.out.println("position out of bound");
        }
    }
	
    //increase all value in linked list by 1
    private static Node<Integer> increment(Node<Integer> head){
        Node<Integer> temp=head;
        while(temp!=null){
            int data=temp.getData();
            data++;
            temp.setData(data);
            temp=temp.getNext();
        }
        return head;
    }
	
    //searching the element (Last encounter)
    private static int findNodeLast(Node<Integer> head,int element){
        Node<Integer> temp=head;
        int pos=-1,count=0;
		
        while (temp!=null) {
            count++;
            if(temp.getData()==element){
                pos=count;
            }
            temp=temp.getNext();
        }
        return pos;
    }
	
    //searching the element (first encounter)
    private static int findNodeFirst(Node<Integer> head,int element){
        Node<Integer> temp=head;
        int pos=0;
        while (temp!=null) {
            if(temp.getData()==element){
                return pos;
            }else{
                temp=temp.getNext();
                pos++;
            }
        }
        return -1;
    }
	
    //append last N nodes to first and return head
    private static Node<Integer> appendLastN(Node<Integer> head,int nth,int length){
        Node<Integer> temp=head,prevR=null,tempL=null,lasNode=null;
        int count=0;
		
        if(nth==0){
            return head;
        }else if(nth>length-1){
            System.out.println("provided position is out of bound");
            return head;
        }
		
        while (temp!=null) {
            if(count==nth){ // for target node
                tempL=temp;
            }else if(count==nth-1 && count!=0){ // for node previous to target node
                prevR=temp;
            }else if(count==length-1){ // for last node
                lasNode=temp;
            }
            count++;
            temp=temp.getNext();
        }
        
        prevR.setNext(null);
        lasNode.setNext(head);
        head=tempL;
		
        return head;
    }
	
    //remove consecutive duplicate nodes
    private static Node<Integer> removeConsecutiveDuplicate(Node<Integer> head){
        Node<Integer> temp=head;
        if(temp==null){
            return head;
        }
        while (temp!=null && temp.getNext() != null) {
            if(temp.getData()==temp.getNext().getData()){
                temp.setNext(temp.getNext().getNext());
            }else{
                temp=temp.getNext();
            }
        }
        return head;
    }
	
    //reverse LL Iteratively 
    private static Node<Integer> reverseLLIteratively(Node<Integer> head){
        Node<Integer> currNode=head,prvNode=null,fwdNode=null;
		
        while (currNode!=null) {
            fwdNode=currNode.getNext(); //1->2 3->4->5->null where 3 is current and 2 is prev ,fwd store next of 3
            currNode.setNext(prvNode);// we make 3 point to 2
            prvNode=currNode; // shift previous node to 1 step forward and make current as new previous
            currNode=fwdNode; // shift current node to 1 step forward and make forward as new current
        }
        head=prvNode; // after loop current reaches null and previous reaches to last node and last node is head of reversed LL
        return head;
    }
	
    //find middle node (returns the node before mid for even length)
    private static Node<Integer> findMid(Node<Integer> head){
        if(head==null) return null;
        Node<Integer> slow=head,fast=head.getNext();
		
        //move slow by one step and fast by two steps, to find mid element , by the end of loop slow is at mid point
        while(fast!=null && fast.getNext()!=null){
            slow=slow.getNext();
            fast=fast.getNext().getNext();
        }
		
        return slow;
    }
	
    //check palindrome
    private static boolean checkPalindrome(Node<Integer> head){
        if(head==null || head.getNext()==null){
            return true; // Empty or single node list is always a palindrome
        }
        // step-1: Find the middle element using slow and fast pointer approach
        Node<Integer> mid=findMid(head);
		
        // step-2: split the list and reverse the second half
        Node<Integer> secondHalf=mid.getNext();
        mid.setNext(null); //This is the crucial step that was missing
		
        // step 2: reverse the second half of the list starting from the mid(slow) node
        secondHalf=reverseLLIteratively(secondHalf);
		
        // step 3 : compare the first and second halves
        Node<Integer> firstHalf=head;
		
        while (secondHalf!=null) {
            if(!firstHalf.getData().equals(secondHalf.getData())){
                return false;
            }
            firstHalf=firstHalf.getNext();
            secondHalf=secondHalf.getNext();
        }
		
        return true;
    }
	
    public static void main(String[] args) {
        Scanner s=new Scanner(System.in);
        Node<Integer> head=takeInput(s); //to take input and create linked list
        printLL(head); // to print linked list
        System.out.println("Length of linked list "+length(head)); //to print length of linked list
        
        System.out.println("Enter position to print value at given position");
        int pos=s.nextInt();
        printAt(head,pos);
		
        System.out.println("Enter position to insert new data at a given position");
        int pos2=s.nextInt();
        System.out.println("Enter the data to be inserted");
        int data2=s.nextInt();
        head=insert(head,pos2,data2);
        printLL(head);
		
        System.out.println("Enter the position of node to be deleted");
        int pos3=s.nextInt();
        head=delete(head, pos3);
        printLL(head);
        
        head=increment(head); // to incease all data values by 1
        printLL(head);
		
        System.out.println("Enter the element you searching for");
        int element=s.nextInt();
        int pos4=findNodeFirst(head,element);
        printAt(head, pos4);
		
        System.out.println("Enter the Nth node");
        int nth=s.nextInt();
        head=appendLastN(head,nth,length(head));
        printLL(head);
		
        head=removeConsecutiveDuplicate(head);
        printLL(head);
		
        head=reverseLLIteratively(head); //to reverse linked list using Iterative method
        
        System.out.println(checkPalindrome(head)); //checking palindrome
		
		
        s.close();
    }
}
```

 **Note :** 

**`temp!= null`**
+ to check that current node is not` null`
+ used when iterating over each node in the list

**`temp.next!= null`** 
+ avoid trying to access **`temp.next`** in body when **`temp`** is the last node in loop

when calling **`temp.next.next`** make sure **`temp.next`** is not `null`


# Slow And Fast pointer approach or **tortoise and hare** algorithm

**Concept:**
- **Slow Pointer**: Moves **1 step** at a time.
- **Fast Pointer**: Moves **2 steps** at a time.

 **Key Applications:**

1. **Cycle Detection**:
    - If there's a cycle, **slow** and **fast** pointers will eventually meet inside the cycle.
    - If there's no cycle, **fast** will reach `null` (end of the list).

2. **Finding the Middle**:
    - For an **odd number** of nodes, **slow** ends up at the middle node.
    - For an **even number** of nodes, **slow** ends up at the **first middle node**.
    - If you need the **second middle node** (for even-length lists), you can adjust the approach slightly by moving the `slow` pointer one extra step when `fast` reaches the end.
    
**Time Complexity**: **O(n)** (Linear time)

**Space Complexity**: **O(1)** (Constant space)

i.e. used in above given code in check palindrome.

## MergeTwoSortedLL (In place sorting)

```java
public class MergeTwoSortedLL {
    
    private static Node<Integer> makeLL(int[] arr){
        Node<Integer> head=null,tail=null;
		
        for(int i=0;i<arr.length;i++){
            Node<Integer> newNode=new Node<Integer>(arr[i]);
            if(head==null){
                head=newNode;
                tail=newNode;
            }else{
                tail.setNext(newNode);
                tail=newNode;
            }
        }
        return head;
    }
	
    private static Node<Integer> mergeLL(Node<Integer> LL1,Node<Integer> LL2){
        if(LL1==null){
            return LL2;
        }else if(LL2==null){
            return LL1;
        }
        Node<Integer> head=null,tail=null,t1=LL1,t2=LL2;
        
        if(t1.getData()<=t2.getData()){
            head=t1;
            tail=t1;
            t1=t1.getNext();
        }else{
            head=t2;
            tail=t2;
            t2=t2.getNext();
        }
        
        while (t1!=null && t2!=null) {
            if(t1.getData()<=t2.getData()){
                tail.setNext(t1);
                tail=t1;
                t1=t1.getNext();
            }else{
                tail.setNext(t2);
                tail=t2;
                t2=t2.getNext();
            }
        }
		
        if(t1!=null){
            tail.setNext(t1);
        }
		
        if(t2!=null){
            tail.setNext(t2);
        }
        return head;
    }
	
    private static void print(Node<Integer> head){
        Node<Integer> temp=head;
        while (temp!=null) {
            System.out.print(temp.getData()+"->");
            temp=temp.getNext();
        }
    }
	
    public static void main(String[] args) {
        int[] arr1={1,3,5};
        int[] arr2={2,4,6};
		
        Node<Integer> LL1=makeLL(arr1);
        Node<Integer> LL2=makeLL(arr2);
		
        Node<Integer> LL3=mergeLL(LL1,LL2);
        print(LL3);
    }
}
```


# Implementing Singly Linked List with Recursive Functions

```java
import java.util.Scanner;

public class LinkedListRecursive {
    // Create Linked list using recursion
    private static Node<Integer> makeLLRecursive(Scanner s){
        int data = s.nextInt();
		
        if(data == -1){
            return null;
        }
        Node<Integer> newNode = new Node<Integer>(data);
        newNode.setNext(makeLLRecursive(s));
		
        return newNode;
    }
	
    // Insert node at position using recursion
    private static Node<Integer> insertRecursive(Node<Integer> head, int pos, int data){
        if(pos < 0){ // Prevent insertion at a negative index
            System.out.println("Error: Position can't be negative");
            return head;
        }
		
        if(pos == 0){
            Node<Integer> newNode = new Node<Integer>(data);
            newNode.setNext(head);
            return newNode;
        }
		
        if (head == null) {  // If we reached the end of the list without inserting
            System.out.println("Error: Position out of bounds.");
            return head;
        }
		
        head.setNext(insertRecursive(head.getNext(), pos-1, data));
        return head;
    }
	
    // Delete node at given position
    private static Node<Integer> deleteRecursive(Node<Integer> head, int pos){
        if(pos < 0){
            System.out.println("Error: Position can't be negative");
            return head;
        }
		
        if(head == null){ // This happens when we reach the end of the linked list
            System.out.println("Error: Position is out of bound");
            return null;
        }
		
        if(pos == 0){
            return head.getNext(); // Skip the current node (delete it)
        }
		
        // Recursive case: Move to the next node and decrease the position
        head.setNext(deleteRecursive(head.getNext(), pos-1));
        return head;
    }
	
    // Reverse linked list using recursion
    private static void reverseLLRecursive(Node<Integer> head){
        if(head == null){
            return;
        }
        reverseLLRecursive(head.getNext());
        System.out.println(head.getData());
    }
	
    // Reverse linked list using recursion (different approach)
    private static Node<Integer> reverseLLRecursive2(Node<Integer> head){
        // If the list is empty or has only one element, return the head
        if(head == null || head.getNext() == null){
            return head;
        }
		
        // Reverse the rest of the list recursively
        Node<Integer> reversedHead = reverseLLRecursive2(head.getNext());
		
        // After the recursive call, adjust the pointers
        head.getNext().setNext(head); // Make the next node point to the current node 
        head.setNext(null); // Set the current node's next to null
		
        return reversedHead; // Return the head of the reversed list
    }
	
    // Print Linked list using recursion
    private static void printRecursive(Node<Integer> head){
        if(head == null){
            return;
        }
        System.out.print(head.getData() + "->");
        printRecursive(head.getNext());
    }
	
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
		
        Node<Integer> head = makeLLRecursive(s);
		
        reverseLLRecursive(head); // Reverse linked list using recursion
		
        System.out.println("Enter position to insert new data at a given position (0 to n):");
        int pos1 = s.nextInt();
        System.out.println("Enter the data to be inserted:");
        int data1 = s.nextInt();
        head = insertRecursive(head, pos1, data1);  // Insert at the given position using recursion
		
        System.out.println("Enter the position of the node to be deleted:");
        int pos2 = s.nextInt();
        head = deleteRecursive(head, pos2); // Delete element at the given position
		
        reverseLLRecursive2(head);
		
        printRecursive(head); // Print linked list using recursion
		
        s.close();
    }
}
```


# Implement `MergeSort` on LinkedList
```java
import java.util.Scanner;

public class MergeSortLL {
    // Make linked list
    private static Node<Integer> makeLL(Scanner s) {
        Node<Integer> head = null, tail = null;
        int data = s.nextInt();
		
        while (data != -1) {
            Node<Integer> newNode = new Node<Integer>(data);
            if (head == null) {
                head = newNode;
                tail = newNode;
            } else {
                tail.setNext(newNode);
                tail = newNode;
            }
            data = s.nextInt();
        }
        return head;
    }
	
    // Print linked list
    private static void printLL(Node<Integer> head) {
        Node<Integer> temp = head;
        if (temp == null) {
            return;
        }
        System.out.print(temp.getData());
        if (temp.getNext() != null) {
            System.out.print(" -> ");
        }
        printLL(temp.getNext());
    }
	
    // Find middle node (returns the node before mid for even length)
    private static Node<Integer> findMid(Node<Integer> head) {
        if (head == null) return null;
        Node<Integer> slow = head, fast = head.getNext();
		
        while (fast != null && fast.getNext() != null) {
            slow = slow.getNext();
            fast = fast.getNext().getNext();
        }
		
        return slow;
    }
	
    // Sort and merge two linked lists
    private static Node<Integer> mergeLL(Node<Integer> LL1, Node<Integer> LL2) {
        Node<Integer> head = null, tail = null, t1 = LL1, t2 = LL2;
		
        // Handle case where one of the lists is empty
        if (t1 == null) return t2;
        if (t2 == null) return t1;
		
        // Initial comparison between the two lists
        if (t1.getData() <= t2.getData()) {
            head = t1;
            tail = t1;
            t1 = t1.getNext();
        } else {
            head = t2;
            tail = t2;
            t2 = t2.getNext();
        }
		
        // Merge the remaining list
        while (t1 != null && t2 != null) {
            if (t1.getData() <= t2.getData()) {
                tail.setNext(t1);
                tail = t1;
                t1 = t1.getNext();
            } else {
                tail.setNext(t2);
                tail = t2;
                t2 = t2.getNext();
            }
        }
		
        // Appending the remaining nodes of the non-empty list
        if (t1 != null) tail.setNext(t1);
        if (t2 != null) tail.setNext(t2);
		
        return head;
    }
	
    // Merge sort on linked list
    private static Node<Integer> mergeSortLL(Node<Integer> head) {
        if (head == null || head.getNext() == null) {
            return head;
        }
		
        Node<Integer> mid = findMid(head); // Get middle node
        Node<Integer> partHead2 = mid.getNext();
        mid.setNext(null); // Split the linked list into two parts
		
        Node<Integer> partHead1 = head;
		
        partHead1 = mergeSortLL(partHead1); // Recursively sort first part
        partHead2 = mergeSortLL(partHead2); // Recursively sort second part
        return mergeLL(partHead1, partHead2); // Merge sorted halves
    }
	
    public static void main(String[] args) {
        Scanner s = new Scanner(System.in);
        Node<Integer> head = makeLL(s);
		
        head = mergeSortLL(head);
		
        printLL(head);
        s.close();
    }
}
```


# `java.util.LinkedList`

```java
import java.util.LinkedList;

public class LinkedListExample {

    public static void main(String[] args) {
        
        // Create a LinkedList of integers
        LinkedList<Integer> list = new LinkedList<>();
		
        // addFirst() - Adds an item to the beginning of the list
        list.addFirst(10); // List: [10]
        list.addFirst(20); // List: [20, 10]
        System.out.println("After addFirst(): " + list); // Output: [20, 10]
		
        // addLast() - Adds an item to the end of the list
        list.addLast(30); // List: [20, 10, 30]
        System.out.println("After addLast(): " + list); // Output: [20, 10, 30]
		
        // removeFirst() - Removes an item from the beginning of the list
        list.removeFirst(); // List: [10, 30]
        System.out.println("After removeFirst(): " + list); // Output: [10, 30]
		
        // removeLast() - Removes an item from the end of the list
        list.removeLast(); // List: [10]
        System.out.println("After removeLast(): " + list); // Output: [10]
		
        // getFirst() - Retrieves the item at the beginning of the list
        int first = list.getFirst(); // first = 10
        System.out.println("First element: " + first); // Output: First element: 10
		
        // getLast() - Retrieves the item at the end of the list
        list.addLast(40); // List: [10, 40]
        int last = list.getLast(); // last = 40
        System.out.println("Last element: " + last); // Output: Last element: 40
		
        // Additional methods
		
        // add() - Adds an item to the end of the list (similar to addLast())
        list.add(50); // List: [10, 40, 50]
        System.out.println("After add(): " + list); // Output: [10, 40, 50]
		
        // peekFirst() - Retrieves the first element without removing it (returns null if empty)
        Integer peekFirst = list.peekFirst(); // peekFirst = 10
        System.out.println("Peek First: " + peekFirst); // Output: Peek First: 10
		
        // peekLast() - Retrieves the last element without removing it (returns null if empty)
        Integer peekLast = list.peekLast(); // peekLast = 50
        System.out.println("Peek Last: " + peekLast); // Output: Peek Last: 50
		
        // remove() - Removes the first occurrence of the specified element
        list.remove(Integer.valueOf(40)); // List: [10, 50]
        System.out.println("After remove(Integer): " + list); // Output: [10, 50]
		
        // clear() - Removes all elements from the list
        list.clear(); // List: []
        System.out.println("After clear(): " + list); // Output: []
    }
}
```

# [HashMap](https://www.programiz.com/java-programming/hashmap)
<u><b>Use case Scenario :</b></u>
to Store key value pair

+ unordered, means elements are not placed in the way they entered.
+ provides **constant time complexity** (O(1)) for most operations like **get()**, **put()**, and **containsKey()**.
+ **value-related operations** in a `HashMap` can take more time than **key-related operations**

```java
import java.util.HashMap;

public class HashMapExample {
    public static void main(String[] args) {
        // Creating a HashMap
        HashMap<Integer, String> map = new HashMap<>();
		
        // put(K key, V value) - Adds key-value pairs to the map
        map.put(1, "Apple");
        map.put(2, "Banana");
        map.put(3, "Cherry");
		
        // get(Object key) - Retrieves the value for the given key
        System.out.println("Value for key 2: " + map.get(2)); // Output: Banana
		
        // containsKey(Object key) - Checks if a key exists
        System.out.println("Contains key 3? " + map.containsKey(3)); // Output: true
		
        // containsValue(Object value) - Checks if a value exists
        System.out.println("Contains value 'Apple'? " + map.containsValue("Apple")); // Output: true
		
        // remove(Object key) - Removes an entry by key
        map.remove(1);
        System.out.println("After removing key 1: " + map);
		
        // size() - Returns the number of key-value pairs
        System.out.println("Size of map: " + map.size()); // Output: 2
		
        // isEmpty() - Checks if the map is empty
        System.out.println("Is map empty? " + map.isEmpty()); // Output: false
		
        // keySet() - Returns a set of all keys
        System.out.println("Keys: " + map.keySet()); // Output: [2, 3]
		
        // values() - Returns a collection of all values
        System.out.println("Values: " + map.values()); // Output: [Banana, Cherry]
		
        // entrySet() - Returns a set of key-value pairs
        System.out.println("Entries: " + map.entrySet());
		
        // Iterating using for-each loop
        for (HashMap.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
		
        // clear() - Removes all entries
        map.clear();
        System.out.println("After clearing: " + map); // Output: {}
    }
}
```


---
# Stack

# Stack Implementation using Array

`StackUsingArray.java`
```java
public class StackUsingArray {
    private int data[];
    private int top;
	
    public StackUsingArray() {  // Constructor
        this.data = new int[10];
        this.top = -1;
    }
	
    public StackUsingArray(int capacity) {  // Constructor with capacity parameter
        this.data = new int[capacity];
        this.top = -1;
    }
	
    public boolean isEmpty() {
        return (top == -1);
    }
	
    public int size() {
        return (top + 1);
    }
	
    public int peek() throws StackEmptyException {
        if (size() == 0) {
            StackEmptyException e = new StackEmptyException();
            throw e;
        }
        return data[top];
    }
	
    public void push(int element){
        if (size() == data.length) {
            doubleCapacity();
        }
        this.top++;
        this.data[top] = element;
    }
    
    private void doubleCapacity(){
		int[] temp=data;
		data=new int[temp.length*2];
		
		for(int i=0;i<temp.length;i++){
			data[i]=temp[i];
		}
	}
	
    public int pop() throws StackEmptyException {
        if (size() == 0) {
            StackEmptyException e = new StackEmptyException();
            throw e;
        }
        int temp = data[top];
        top--;
        return temp;
    }
}
```

`StackFullException.java`
```java
public class StackFullException extends Exception {
}
```

`StackEmptyException.java`
```java
public class StackEmptyException extends Exception {

}
```

`StackUse.java`
```java
public class StackUse {
    public static void main(String[] args) throws StackFullException {
        StackUsingArray s1 = new StackUsingArray();
        
        // Push elements into the stack
        for (int i = 1; i <= 5; i++) {
            s1.push(i);
        }
		
        // Pop elements from the stack and print them
        while (!s1.isEmpty()) {
            try {
                System.out.println(s1.pop());
            } catch (Exception e) {
                // Handle any exceptions (though unlikely in this example)
            }
        }
    }
}
```


# Stack Implementation using Linked List

`Node.java`
```java
public class Node<T> {
    private T data;
    private Node<T> next;
	
    public Node(T data){
        this.data = data;
        this.next = null;
    }
	
    public void setData(T data){
        this.data = data;
    }
	
    public void setNext(Node<T> next){
        this.next = next;
    }
	
    public T getData(){
        return this.data;
    }
	
    public Node<T> getNext(){
        return this.next;
    }
}
```

`StackUsingLL.java`
```java
public class StackUsingLL<T> {
    private Node<T> head;
    private int size;
	
    public StackUsingLL(){
        this.head = null;
        size = 0;
    }
	
    public int size(){
        return size;
    }
	
    public T top() throws StackEmptyException {
        if(size == 0){
            throw new StackEmptyException();
        }
        return head.getData();
    }
	
    public boolean isEmpty(){
        // return (size == 0 ? true : false );
        return (size == 0);
    }
	
    public void push(T data){
        Node<T> newNode = new Node<>(data);
        newNode.setNext(head); // make the new node point to the old head
        head = newNode;  // update head to the new node
        size++;
    }
	
    public T pop() throws StackEmptyException {
        if(size == 0){
            throw new StackEmptyException();
        }
        T data = head.getData();
        head = head.getNext();
        size--;
        return data;
    }
}
```

`StackEmptyException.java`
```java
public class StackEmptyException extends Exception {

}
```

`StackUsingLLUse.java`
```java
public class StackUsingLLUse {
    public static void main(String[] args) {
        StackUsingLL<Integer> s1 = new StackUsingLL<>();
        // push data into stack
        for (int i = 0; i < 3; i++) {
            s1.push(i + 1);
        }
		
        // pop data from stack
        while (!s1.isEmpty()) {
            try {
                System.out.println(s1.pop());
            } catch (Exception e) {
                // TODO: handle exception
            }
        }
    }
}
```


# [`java.util.Stack`](https://www.programiz.com/java-programming/stack)

```java
import java.util.Stack;

public class StackExample {
    public static void main(String[] args) {
        Stack<Integer> s1 = new Stack<>();
		
        // Push elements onto the stack
        s1.push(10);  // Adds 10 to the stack
        s1.push(20);  // Adds 20 to the stack
        s1.push(30);  // Adds 30 to the stack
        System.out.println("Stack after pushes: " + s1);  // Prints the stack
		
        // Peek at the top element (without removing it)
        System.out.println("Top element: " + s1.peek());  // Prints the top element (30)
		
        // Pop an element from the stack (removes and returns it)
        int poppedElement = s1.pop();
        System.out.println("Popped element: " + poppedElement);  // Pops and prints 30
        System.out.println("Stack after pop: " + s1);  // Prints the updated stack
		
        // Check if the stack is empty
        System.out.println("Is stack empty? " + s1.isEmpty());  // Prints false
		
        // Check the size of the stack
        System.out.println("Size of stack: " + s1.size());  // Prints the size (2 in this case)
		
        // Search for an element in the stack (returns the 1-based index)
        int position = s1.search(20);  
        System.out.println("Position of 20 in stack: " + position);  // Prints the position (1-based)
		
        // Try popping all elements
        while (!s1.isEmpty()) {
            System.out.println("Popped element: " + s1.pop());
        }
        System.out.println("Stack after popping all elements: " + s1);  // Should print an empty stack
    }
}
```



# Queue 

# Queue Implementation using Array

```java
public class QueueUsingArray {
    private int[] data;
    private int rear;
    private int front;
    private int size;
	
    public QueueUsingArray() {
        this.data = new int[10];
        this.rear = -1;
        this.front = -1;
        this.size = 0;
        // Note: default capacity is set to 10
    }
	
    public QueueUsingArray(int capacity) {
        this.data = new int[capacity];
        this.rear = -1;
        this.front = -1;
        this.size = 0;
        // Note: allows creating queue with custom initial capacity
    }
	
    public boolean isEmpty() {
        return (size == 0);
        // Note: simple check using size field for constant time operation
    }
	
    public int size() {
        return size;
        // Note: size tracks the current number of elements in the queue
    }
	
    public int front() throws QueueEmptyException {
        if (front == -1) {
            throw new QueueEmptyException();
            // Note: -1 front indicates the queue is empty
        }
        return data[front];
        // Note: returns element at front index without removing it
    }
	
    public void enqueue(int data) throws QueueFullException {
        if (size == this.data.length) {
            // throw new QueueFullException();
            doubleCapacity(); // dynamically increases capacity instead of throwing an error
        }
        if (size == 0) { // first element added, front must be initialized
            front = 0;
        }
		
        size++;
        // rear = (rear + 1) % this.data.length; instead of below rear++ and if we can write this
        rear++;
        if (this.rear == this.data.length) { // handles circular indexing manually
            rear = 0;
        }
        
        this.data[rear] = data; // assigns new data at the calculated rear position
    }
	
    private void doubleCapacity() {
        int[] temp = data;
        data = new int[temp.length * 2];
        int index = 0;
		
        // this copy data from front to last
        for (int i = front; i < temp.length; i++) {
            data[index] = temp[i];
            index++;
        }
		
        // this copy data from start to front-1
        for (int i = 0; i <= front - 1; i++) {
            data[index] = temp[i];
            index++;
        }
		
        front = 0;
        rear = temp.length;
        // Note: resets front to 0 and rear to the last valid index in old array
        // Now queue is linear in memory again
    }
	
    public int dequeue() throws QueueEmptyException {
        if (front == -1) {  // underflow check - queue is empty
            throw new QueueEmptyException();
        }
		
        int temp = data[front];
		
        // front = (front + 1) % this.data.length; instead of below front++ and if we can write this
        front++;
        if (this.front == this.data.length) { // handles circular increment of front
            front = 0;
        }
		
        size--;
		
        if (size == 0) { // reset queue if it becomes empty
            front = -1;
            rear = -1;
        }
		
        return temp; // returns the removed element
    }
}
```

```java
public class QueueFullException extends Exception{
	
	public QueueFullException(){
		super("Queue is full");
	}
}
```

```java
public class QueueEmptyException extends Exception{
	
	public QueueEmptyException(){
		super("Queue is empty");
	}
}
```

```java
public class QueueUse {
    public static void main(String[] args) {
        QueueUsingArray q1 = new QueueUsingArray();
		
        // Enqueue elements
        for (int i = 1; i <= 10; i++) {
            try {
                q1.enqueue(i);
            } catch (QueueFullException e) {
                System.out.println("Failed to enqueue " + i + ": " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Unexpected error during enqueue: " + e.getMessage());
            }
        }
		
        // Dequeue elements
        while (!q1.isEmpty()) {
            try {
                System.out.println(q1.dequeue());
            } catch (QueueEmptyException e) {
                System.out.println("Failed to dequeue: " + e.getMessage());
            } catch (Exception e) {
                System.out.println("Unexpected error during dequeue: " + e.getMessage());
            }
        }
    }
}
```


# Queue Implementation using Linked List

`Node.java`
```java
public class Node<T> {
    private T data;
    private Node<T> next;
	
    public Node(T data){
        this.data = data;
        this.next = null;
    }
	
    public void setData(T data){
        this.data = data;
    }
	
    public void setNext(Node<T> next){
        this.next = next;
    }
	
    public T getData(){
        return this.data;
    }
	
    public Node<T> getNext(){
        return this.next;
    }
}
```


```java
public class QueueUsingLL<T> {
    private Node<T> front;
    private Node<T> rear;
    private int size;
	
    public QueueUsingLL() {
        this.front = null;
        this.rear = null;
        this.size = 0;
    }
	
    public int size() {
        return this.size;
    }
	
    public boolean isEmpty() {
        return (size == 0);
    }
	
    public T front() throws Exception {
        if (size == 0) { // when list is empty
            throw new Exception("Queue is empty");
        }
        return front.getData();
    }
	
    public void enqueue(T data) {
        Node<T> newNode = new Node<T>(data);
        if (this.rear == null) {
            front = newNode;
            rear = newNode;
        } else {
            rear.setNext(newNode);
            rear = newNode;
        }
        size++;
    }
	
    public T dequeue() throws Exception {
        if (size == 0) { // when list is empty
            throw new Exception("Queue is empty");
        }
        T temp = front.getData();
        front = front.getNext();
        if (size == 1) { // when removing last element
            front = null;
            rear = null;
        }
        size--;
		
        return temp;
    }
}
```


```java
public class QueueUse {
    public static void main(String[] args) {
        QueueUsingLL<Integer> q1 = new QueueUsingLL<>();
        
        for (int i = 1; i <= 10; i++) {
            q1.enqueue(i);
        }
		
        while (!q1.isEmpty()) {
            try {
                System.out.println(q1.dequeue());
            } catch (Exception e) {
                // TODO: handle exception
                System.out.println(e.getMessage());
            }
        }
    }
}
```



# [`java.util.queue`](https://www.programiz.com/java-programming/queue)

Since the Queue is an interface, we cannot provide the direct implementation of it.

In order to use the functionalities of Queue, we need to use classes that implement it:
+ `ArrayDeque`
+ `LinkedList`
+ `PriorityQueue`

```java
import java.util.*;

public class QueueExample {
    public static void main(String[] args) {
        Queue<String> q = new LinkedList<>();
		
        // 1️⃣ add() – Adds element, throws exception if fails
        q.add("A");
        q.add("B");
		
        // 2️⃣ offer() – Adds element, returns false if fails (better for capacity-restricted queues)
        q.offer("C");
		
        // Queue: [A, B, C]
		
        // 3️⃣ peek() – Returns head without removing, returns null if empty
        System.out.println("Peek: " + q.peek()); // Output: A
		
        // 4️⃣ element() – Same as peek() but throws exception if empty
        System.out.println("Element: " + q.element()); // Output: A
		
        // 5️⃣ poll() – Removes and returns head, returns null if empty
        System.out.println("Poll: " + q.poll()); // Output: A
		
        // 6️⃣ remove() – Removes and returns head, throws exception if empty
        System.out.println("Remove: " + q.remove()); // Output: B
		
        // Remaining Queue: [C]
        System.out.println("Queue: " + q); // Output: [C]
    }
}
```




# Tree

# Tree implementation using ArrayList

```java
import java.util.ArrayList;

public class TreeNode<T> {
    public T data;
    public ArrayList<TreeNode<T>> children;
	
    public TreeNode(T data){
        this.data = data;
        children = new ArrayList<>();
    }
}
```

```java
public class TreeUse {
    public static void main(String[] args) {
        TreeNode<Integer> root = new TreeNode<Integer>(4);
        TreeNode<Integer> node1 = new TreeNode<Integer>(2);
        TreeNode<Integer> node2 = new TreeNode<Integer>(3);
        TreeNode<Integer> node3 = new TreeNode<Integer>(5);
        TreeNode<Integer> node4 = new TreeNode<Integer>(6);
        
        root.children.add(node1);
        root.children.add(node2);
        root.children.add(node3);
		
        node2.children.add(node4);
    }
}
```


```java
import java.util.*; // added for Queue

public class TreeUse {
    
    // DFS-style recursive tree input
    public static TreeNode<Integer> takeInput() {
        Scanner s = new Scanner(System.in);
        
        // Ask for node data
        System.out.println("Enter next node data");
        int r = s.nextInt();
        
        // Create current node
        TreeNode<Integer> root = new TreeNode<Integer>(r);
        
        // Ask how many children this node has
        System.out.println("Enter number of children for " + r);
        int childCount = s.nextInt();
		
        // Recursively build child subtrees
        for (int i = 0; i < childCount; i++) {
            TreeNode<Integer> child = takeInput();
            root.children.add(child);
        }
		
        return root;
    }
	
    // DFS-style tree printing (flat view)
    private static void print(TreeNode<Integer> root) {
        String s = root.data + ":";
		
        // Append all immediate children
        for (int i = 0; i < root.children.size(); i++) {
            s = s + root.children.get(i).data + ",";
        }
        System.out.println(s);
		
        // Recursively print each child subtree
        for (int i = 0; i < root.children.size(); i++) {
            print(root.children.get(i));
        }
    }
	
    // ASCII Tree Printer (Pretty structure view)
    public static void printBetter(TreeNode<Integer> root) {
        printBetterHelper(root, "", true);
    }
	
    /**
     * Recursively prints tree with ASCII branches
     * 
     * @param node Current node
     * @param prefix Indentation + lines to show depth/branching
     * @param isTail True if node is last child (for └──), else false (for ├──)
     */
    private static void printBetterHelper(TreeNode<Integer> node, String prefix, boolean isTail) {
        if (node == null) return;
		
        // Print current node with proper branch symbol
        System.out.println(prefix + (isTail ? "└── " : "├── ") + node.data);
		
        // Handle all children except the last
        for (int i = 0; i < node.children.size() - 1; i++) {
            printBetterHelper(node.children.get(i), prefix + (isTail ? "    " : "│   "), false);
        }
		
        // Handle last child with a └──
        if (node.children.size() > 0) {
            printBetterHelper(node.children.get(node.children.size() - 1), prefix + (isTail ? "    " : "│   "), true);
        }
    }
	
    // BFS-style tree print (level-wise display)
    public static void printLevelWise(TreeNode<Integer> root) {
        if (root == null) return;
		
        Queue<TreeNode<Integer>> queue = new LinkedList<>();
        queue.add(root);
		
        while (!queue.isEmpty()) {
            TreeNode<Integer> currentNode = queue.poll();
            String output = currentNode.data + ":";
			
            for (int i = 0; i < currentNode.children.size(); i++) {
                output += currentNode.children.get(i).data;
                if (i != currentNode.children.size() - 1) {
                    output += ",";
                }
                queue.add(currentNode.children.get(i));
            }
			
            System.out.println(output);
        }
    }
	
    // count total number of nodes in tree
    private static int numNodes(TreeNode<Integer> root){
        if(root == null){
            return 0;
        }
        return numNodesHelper(root);
    }

    private static int numNodesHelper(TreeNode<Integer> root){
        int count = 1;
        for(int i = 0; i < root.children.size(); i++){
            count += numNodes(root.children.get(i));
        }
        return count;
    }

    // sum of all nodes
    private static int sumOfNodes(TreeNode<Integer> root){
        if(root == null) return 0;

        int sum = 0;
        sum += root.data;
        for(int i = 0; i < root.children.size(); i++){
            sum += sumOfNodes(root.children.get(i));
        }
        return sum;
    }

    // find node with maximum value
    private static int maxNode(TreeNode<Integer> root){
        if(root == null) return Integer.MIN_VALUE;
        
        int max = root.data;
        for(TreeNode<Integer> child : root.children){
            max = Math.max(max, maxNode(child));
        }
        return max;
    }

    // returns number of nodes greater than the given number
    private static int numNodesGreater(TreeNode<Integer> root){
        Scanner s = new Scanner(System.in);
        int num = s.nextInt();
        return numNodesGreaterHelper(root, num);
    }
    
    private static int numNodesGreaterHelper(TreeNode<Integer> root, int num){
        if (root.data == null) return 0;

        int count = 0;
        if (root.data > num) count++;

        for(TreeNode<Integer> child : root.children) {
            count += numNodesGreaterHelper(child, num);
        }
        return count;
    }

    // calculates height of the tree
    private static int getHeight(TreeNode<Integer> root) {
        if (root == null) return 0;
    
        int maxChildHeight = 0; // Track tallest child height
    
        for (TreeNode<Integer> child : root.children) {
            int childHeight = getHeight(child);
            maxChildHeight = Math.max(maxChildHeight, childHeight);
        }
    
        return maxChildHeight + 1; // Height = 1 (self) + tallest child
    }
    
    // Entry point of program
    public static void main(String[] args) {
        TreeNode<Integer> root = takeInput();
        
        System.out.println("Basic Tree Print");
        print(root); // DFS-style flat tree print
        
        System.out.println("ASCII Tree Print");
        printBetter(root); // Tree structure with branches
        
        System.out.println("Level-wise Tree Print");
        printLevelWise(root); // BFS-style level-wise print

        System.out.println("Number of nodes");
        System.out.println(numNodes(root)); // print number of nodes

        System.out.println("Sum of all nodes");
        System.out.println(sumOfNodes(root)); // print sum of all nodes

        System.out.println("Largest node");
        System.out.println(maxNode(root)); // print node with maximum value

        System.out.println("Number of nodes greater than given value");
        System.out.println(numNodesGreater(root)); // print number of nodes greater than the given value

        System.out.println("Height of tree");
        System.out.println(getHeight(root)); // print height of tree
    } 
}
```

Above `printBetter` use ASCII **branches like └──, ├──, │**. to print tree
i.e.
└── 1
    ├── 2
    │   ├── 4
    │   └── 5
    └── 3

`private static void printBetterHelper(TreeNode<Integer> node, String prefix, boolean isTail)`

`printBeterHelper` is just a wrapper function. It calls the recursive helper with:

 Parameters:
- **`node`** – Current node we’re printing.
- **`prefix`** – Indentation + lines (`│` or   ) that represent vertical branches.
- **`isTail`** – Is this node the last child of its parent? (Used to decide whether to draw `└──` or `├──`






