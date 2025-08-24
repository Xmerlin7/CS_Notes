# Explanation

+ A stack is a collection that is based on the last-in-first-out (LIFO) policy.
![[Operations on a pushdown stack.png|300]]

# Implementation
+ Array Based implementation: 
```Javascript 
class stack {

  constructor() {

    this.items = [];

    this.counter = 0;

  }

  push(element) {

    this.items[this.counter] = element;

    this.counter++;

    console.log(

      `this number ${this.items[this.counter - 1]} has been added out of ${

        this.counter

      }`

    );

    return this.items[this.counter - 1];

  }

  pop() {

    if (this.counter === 0) {

      console.log("Stack is empty");

      return;

    }

    const removedElement = this.items[this.counter - 1];

    this.items[this.counter - 1] = undefined;

    console.log(

      `this number ${removedElement} has been deleted out of ${this.counter}`

    );

    this.counter--;

    return removedElement;

  }

  isEmpty() {

    return this.counter === 0;

  }

  

  // Get the size of the stack

  size() {

    return this.counter;

  }

  peek() {

    if (this.isEmpty()) {

      console.log("Stack is empty");

      return null;

    }

    console.log(`last number is ${this.items[this.counter - 1]}`);

    return this.items[this.counter -1];

  }

  print(){

    console.log(`stack: ${this.items.filter(x => x != undefined).join(" -> ")}`)

  }

}

let stackey = new stack();

  

stackey.push(5);

stackey.push(10);
stackey.pop();

stackey.peek();

stackey.print()
```
+ Linked-list implementation:
```java
public class Stack<Item> implements Iterable<Item> 
{
	private Node first;  // top of stack (most recently added node)
	private int N;       // number of items
	private class Node
	{   // nested class to define nodes
        Item item; 
        Node next; 
    }

	public boolean isEmpty() { return first == null; }    // Or: N == 0.
	public int size()        { return N;             } 
	public void push(Item item)
	{   // Add item to top of stack.
		Node oldfirst = first; 
		first = new Node(); 
		first.item = item; 
		first.next = oldfirst; 
		N++; 
	} 
	
	public Item pop()
	{   // Remove item from top of stack.
		Item item = first.item; 
		first = first.next; 
		N--; 
		return item; 
	}
}
```
# Sources
+ [Princeton University: Algorithms part | - Lecture 3 ](https://www.coursera.org/learn/algorithms-part1/lecture/jSxyD/stacks)
+ Algorithms 1.3