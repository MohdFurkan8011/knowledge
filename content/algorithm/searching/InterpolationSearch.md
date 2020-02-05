# Interpolation Search

Given a sorted array of n uniformly distributed values arr[], write a function to search for a particular element x in the array.

Linear Search finds the element in O(n) time, [Jump Search](https://www.geeksforgeeks.org/jump-search/) takes O(√ n) time and [Binary Search](http://quiz.geeksforgeeks.org/binary-search/) take O(Log n) time.
The Interpolation Search is an improvement over [Binary Search](http://quiz.geeksforgeeks.org/binary-search/) for instances, where the values in a sorted array are uniformly distributed. Binary Search always goes to the middle element to check. On the other hand, interpolation search may go to different locations according to the value of the key being searched. For example, if the value of the key is closer to the last element, interpolation search is likely to start search toward the end side.

To find the position to be searched, it uses following formula.

#### The complexity of Interpolation Search Technique

1. **Time Complexity:** O(log2(log2 n)) for the average case, and O(n) for the worst case (when items are distributed exponentially)
2. **Space Complexity:** O(1)

```java
class Test { 
    // Array of items on which search will 
    // be conducted. 
    static int arr[] = new int[]{10, 12, 13, 16, 18, 19, 20, 21, 22, 23, 24, 33, 35, 	
                                 42, 47}; 
     
    // If x is present in arr[0..n-1], then returns 
    // index of it, else returns -1. 
    static int interpolationSearch(int x) { 
        // Find indexes of two corners 
        int lo = 0, hi = (arr.length - 1); 
      
        // Since array is sorted, an element present 
        // in array must be in range defined by corner 
        while (lo <= hi && x >= arr[lo] && x <= arr[hi]) {         
 
            if (lo == hi) { 
                if (arr[lo] == x) return lo; 
                return -1; 
            } 
        
            // Probing the position with keeping 
            // uniform distribution in mind. 
             
            int pos = lo + (((hi-lo) / 
                  (arr[hi]-arr[lo]))*(x - arr[lo])); 
      
            // Condition of target found 
            if (arr[pos] == x) 
                return pos; 
      
            // If x is larger, x is in upper part 
            if (arr[pos] < x) 
                lo = pos + 1; 
      
            // If x is smaller, x is in the lower part 
            else
                hi = pos - 1; 
        } 
        return -1; 
    } 
   
    // Driver method  
    public static void main(String[] args)  { 
        int x = 18; // Element to be searched 
        int index = interpolationSearch(x); 
          
         // If element was found 
        if (index != -1) 
            System.out.println("Element found at index " + index); 
       	else
        	System.out.println(``"Element not found."``); 
    } 
} 
```