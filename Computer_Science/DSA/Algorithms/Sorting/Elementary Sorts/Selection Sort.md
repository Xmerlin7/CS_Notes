# Explanation

+ Selection sort works as follows: 
	1. Find the smallest item in the array and exchange it with the first entry (itself if the first entry is already the smallest). 
	2. Find the next smallest item and exchange it with the second entry. 
	3. Continue in this way until the entire array is sorted.
# Selection Sort Implementation
```java
const unsortedArray = [34, 7, 23, 32, 5, 62, -9, -1, 45, 19];

  

const smallest = findSmallest(unsortedArray);

console.log(unsortedArray[smallest]);

  

function findSmallest(arr) {

  let smallest = arr[0];

  let smallestIndex = 0;

  for (let i = 1; i < arr.length; i++) {

    // Changed loop condition

    if (arr[i] < smallest) {

      smallest = arr[i];

      smallestIndex = i;

    }

  }

  return smallestIndex;

}

  

function selectionSort(arr) {

  let newArr = [];

  const originalLength = arr.length; // Avoid dynamic length changes

  for (let i = 0; i < originalLength; i++) {

    // Corrected loop

    let smallest = findSmallest(arr);

    newArr.push(arr.splice(smallest, 1)[0]); // Extract the value from the returned array

  }

  return newArr;

}

  

console.log(selectionSort(unsortedArray));
```
# Analysis
+ Selection sort uses ~$N^2/2$ compares and N exchanges to sort an array of length N.
+ Running time is insensitive to input: it takes about as long to run selection sort for an array that is already in order or for an array with all keys equal as it does for a randomly-ordered array.
+ The number of array accesses is a linear function of the array size.
# Sources
+ [Princeton University: Algorithms part | - Lecture 4 ](https://www.coursera.org/learn/algorithms-part1/lecture/VE0sv/selection-sort)
+ Algorithms 2.1