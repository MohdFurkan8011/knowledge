# Binary Search

**Binary search** is the most popular Search algorithm. It is efficient and also one of the most commonly used techniques that is used to solve problems.

Binary search works only on a sorted set of elements. To use binary search on a collection, the collection must first be sorted.

In this procedure, the entire list is divided into two sub-lists. If the item is found in the middle position, it returns the location, otherwise jumps to either left or right sub-list and do the same process again until finding the item or exceed the range.

#### The complexity of Binary Search Technique

1. **Time Complexity****:** O(1) for the best case. O(log2 n) for average or worst case.
2. **Space Complexity:** O(1) 



```java
class BinarySearch { 
    // Returns index of x if it is present in arr[l.. 
    // r], else return -1 
    int binarySearch(int arr[], int l, int r, int x) { 
        if (r >= l) { 
        	int mid = l + (r - l) / 2; 
 
            // If the element is present at the 
            // middle itself 
            if (arr[mid] == x) 
                return mid; 
 
            // If element is smaller than mid, then 
            // it can only be present in left subarray 
            if (arr[mid] > x) 
                return binarySearch(arr, l, mid - 1, x); 
 
            // Else the element can only be present 
            // in right subarray 
            return binarySearch(arr, mid + 1, r, x); 
        } 
 
        // We reach here when element is not present 
        // in array 
        return -1; 
    } 
 
    // Driver method to test above 
    public static void main(String args[]) { 
        
        BinarySearch ob = ``new` `BinarySearch(); 
        int arr[] = {2, 3, 4, 10, 40}; 
        int n = arr.length; 
        int x = 10; 
        int result = ob.binarySearch(arr, 0, n - 1, x); 
        if (result == -1) 
            System.out.println("Element not present"); 
        else
            System.out.println("Element found at index " + result); 
    } 
} 
```