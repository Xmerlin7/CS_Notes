# Explanation

+ A queue is a collection that is based on the first-in-first-out (FIFO) policy.
# Implementation
+ Linked-list implementation:
```Javascript 

class queue {

  constructor() {

    this.items = [];

    this.counter = 0;

  }

  enqueue(element) {

    this.items[this.counter] = element;

    this.counter++;

    console.log(this.items.filter((x) => x != null).join("- >"));

    return element;

  }

  isEmpty() {

    return this.counter === 0;

  }

  dequeue() {

    if (this.isEmpty()) {

      console.log("Queue is empty");

      return null;

    }

    let deletedItem = this.items.shift();

    console.log(`this is the deleted item ${deletedItem}`);

    this.counter--;

    return deletedItem;

  }

  peek() {

    console.log(`this is the queue first element ${this.items[0]}`);

  }

  size() {

    console.log(`this is the queue size ${this.counter}`);

  }

  print() {

    console.log(this.items.filter((x) => x != null).join("- >"));

  }

}

let queuee = new queue();

queuee.enqueue(7);

queuee.enqueue(6);

queuee.dequeue();

queuee.print();

queuee.size();

queuee.peek();

```
# Sources
+ [Princeton University: Algorithms part | - Lecture 3 ](https://www.coursera.org/learn/algorithms-part1/lecture/5vgrm/queues)
+ Algorithms 1.3