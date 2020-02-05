# Expontial Search

The name of this searching algorithm may be misleading as it works in O(Log n) time. The name comes from the way it searches an element.

#### The complexity of Exponential Search Technique

1. **Time Complexity:** O(1) for the best case. O(log2 i) for average or worst case. Where i is the location where search key is present.
2. **Space Complexity:** O(1)

1. Find range where element is present
2. Do Binary Search in above found range.

**How to find the range where element may be present?**
The idea is to start with subarray size 1, compare its last element with x, then try size 2, then 4 and so on until last element of a subarray is not greater.
Once we find an index i (after repeated doubling of i), we know that the element must be present between i/2 and i (Why i/2? because we could not find a greater value in previous iteration)

Given below are the implementations of above steps.

```java
class GFG { 
    // Returns position of first occurrence of 
    // x in array 
    static int exponentialSearch(int arr[], int n, int x) { 
        // If x is present at firt location itself 
        if (arr[0] == x) 
            return 0; 
     
        // Find range for binary search by 
        // repeated doubling 
        int i = 1; 
        while (i < n && arr[i] <= x) 
            i = i*2; 
     
        // Call binary search for the found range. 
        return Arrays.binarySearch(arr, i/2, Math.min(i, n), x); 
    } 
     
    // Driver code 
    public static void main(String args[]) { 
        int arr[] = {2, 3, 4, 10, 40}; 
        int x = 10; 
        int result = exponentialSearch(arr, arr.length, x); 
         
        System.out.println((result < 0) ?  
                            "Element is not present in array": 
                            "Element is present at index "+ result); 
    } 
} 
```