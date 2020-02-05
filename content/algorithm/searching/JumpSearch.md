# Jump Search

Jump search technique also works for ordered lists. It creates a block and tries to find the element in that block. If the item is not in the block, it shifts the entire block. The block size is based on the size of the list. If the size of the list is n then block size will be √n. After finding a correct block it finds the item using a linear search technique. The jump search lies between linear search and binary search according to its performance.

#### The complexity of Jump Search Technique

1. Time Complexity: O(√n)
2. Space Complexity: O(1)

```java
public class JumpSearch { 
    public static int jumpSearch(int[] arr, int x)  { 
        int n = arr.length; 
 
        // Finding block size to be jumped 
        int step = (int)Math.floor(Math.sqrt(n)); 
 
        // Finding the block where element is 
        // present (if it is present) 
        int prev = 0; 
        while (arr[Math.min(step, n)-1] < x)  {
            prev = step; 
            step += (int)Math.floor(Math.sqrt(n)); 
            if(prev >= n) 
            	return -1; 
        } 
 
        // Doing a linear search for x in block 
        // beginning with prev. 
        while (arr[prev] < x) { 
            prev++; 
 
            // If we reached next block or end of 
            // array, element is not present. 
            if (prev == Math.min(step, n)) 
				return -1; 
        } 
 
        // If element is found 
        if (arr[prev] == x) 
            return prev; 
 
        return -1; 
    } 
 
    // Driver program to test function 
    public static void main(String [ ] args) { 
        int arr[] = {0, 1, 1, 2, 3, 5, 8, 13, 21, 34, 55, 89, 144, 233, 377, 610}; 
        int x = 55; 
 
        // Find the index of 'x' using Jump Search 
        int index = jumpSearch(arr, x); 
 
        // Print the index where 'x' is located 
        System.out.println("\nNumber " + x + " is at index " + index); 
    } 
} 
```

