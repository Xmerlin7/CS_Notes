for any list of n, <span style="color:#00b050">Binary Search</span> will take $log2 n$ steps to run in the worst case

![[Pasted image 20241006191801.png]]
Too low, but you just eliminated half the numbers! Now you know that 1–50 are all too low. Next guess: 75.
![[Pasted image 20241006191835.png]]
Too high, but again you cut down half the remaining numbers! With binary search, you guess the middle number and eliminate half the remaining numbers every time. Next is 63 (halfway between 50 and 75).
![[Pasted image 20241006191923.png]]
This is binary search. You just learned your first algorithm! Here’s how many numbers you can eliminate every time.
![[Pasted image 20241006191935.png]]
`low = 0` 
`high = len(list) - 1`
![[Pasted image 20241006192028.png]]
```javascript
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9]

console.log(binarySearch(arr, 9))

function binarySearch(arr, element) {
    let left = 0
    let right = arr.length - 1

    while (left <= right) {

        let mid = Math.floor((left + right) / 2);
        
        let guess = arr[mid]
        
        if (guess === element)
            return mid
            
        if (guess > element)
            right = mid - 1
        else
            left = mid + 1
    }

    return (-1)

}
```