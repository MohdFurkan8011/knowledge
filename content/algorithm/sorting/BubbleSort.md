# Bubble Sort

Bubble sort is a simple sorting algorithm. This sorting algorithm is comparison-based algorithm in which each pair of adjacent elements is compared and the elements are swapped if they are not in order. This algorithm is not suitable for large data sets.

Following are the time and space complexity for the Bubble Sort algorithm.

- Worst Case Time Complexity [ Big-O ]: **O(n2)**
- Best Case Time Complexity [Big-omega]: **O(n)**
- Average Time Complexity [Big-theta]: **O(n2)**
- Space Complexity: **O(1)**

```java
void bubble_sort( int A[ ], int n ) {
    // to check given array is already sorted to reduce complexity
    int isSorted = true;
    for(int k = 0; k< n-1; k++) {
        // (n-k-1) is for ignoring comparisons of elements which have already been 
        // compared in earlier iterations
        for(int i = 0; i < n-k-1; i++) {
            if(A[ i ] > A[ i+1] ) {
                // here swapping of positions is being done.
                int temp = A[ i ];
                A[ i ] = A[ i+1 ];
                A[ i + 1] = temp;
                isSorted = false;
            }
        }
        if (isSorted) {
 			break;           
        }
    }
}
```

