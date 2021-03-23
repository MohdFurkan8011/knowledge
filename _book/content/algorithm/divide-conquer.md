# Divide and Conquer

Divide and Conquer is an algorithmic pattern. In algorithmic methods, the design is to take a dispute on a huge input, break the input into minor pieces, decide the problem on each of the small pieces, and then merge the piecewise solutions into a global solution. This mechanism of solving the problem is called the Divide & Conquer Strategy.

Divide and Conquer algorithm consists of a dispute using the following three steps.

1. **Divide** the original problem into a set of subproblems.

2. **Conquer:** Solve every subproblem individually, recursively.

3. **Combine:** Put together the solutions of the subproblems to get the solution to the whole problem.

   ![divide-conquer](..\images\divide-conquer.PNG)





The specific computer algorithms are based on the Divide & Conquer approach

- [Maximum and Minimum Problem](#maximum-and-minimum-problem)
- [Binary Search](../algorithm/searching/BinarySearch.md)
- [Merge and Quick Sorting](../algorithm/sorting/README.md)
- [Tower of Hanoi]()



##### Maximum and Minimum Problem

```java
public class MaxMinProblem {

    static class Pair { 
        int min;
        int max;
    }
 
    static Pair getMinMax(int arr[], int low, int high) {
        Pair minmax = new Pair();
                 
        // If there is only one element 
        if (low == high) {
            minmax.max = arr[low];
            minmax.min = arr[low];
            return minmax;
        }
 
        /* If there are two elements */
        if (high == low + 1) {
            if (arr[low] > arr[high]) {
                minmax.max = arr[low];
                minmax.min = arr[high];
            } else {
                minmax.max = arr[high];
                minmax.min = arr[low];
            }
            return minmax;
        }
 
        /* If there are more than 2 elements */
        int mid = (low + high) / 2;
        Pair mml = getMinMax(arr, low, mid);
		Pair mmr = getMinMax(arr, mid + 1, high);
 
        /* compare minimums of two parts*/
        if (mml.min < mmr.min) {
            minmax.min = mml.min;
        } else {
            minmax.min = mmr.min;
        }
 
        /* compare maximums of two parts*/
        if (mml.max > mmr.max) {
            minmax.max = mml.max;
        } else {
            minmax.max = mmr.max;
        }
 
        return minmax;
    }
 
    /* Driver program to test above function */
    public static void main(String args[]) {
        int arr[] = {1000, 11, 445, 1, 330, 3000};
        int arr_size = 6;
        Pair minmax = getMinMax(arr, 0, arr_size - 1);
        System.out.printf("\nMinimum element is %d", minmax.min);
        System.out.printf("\nMaximum element is %d", minmax.max);
 
    }
}
```



##### **Tower of  Hanoi**

```java
class GFG 
{ 
    // Java recursive function to solve tower of hanoi puzzle 
    static void towerOfHanoi(int n, char from_rod, char to_rod, char aux_rod) 
    { 
        if (n == 1) 
        { 
            System.out.println("Move disk 1 from rod " +  from_rod + " to rod " + to_rod); 
            return; 
        } 
        towerOfHanoi(n-1, from_rod, aux_rod, to_rod); 
        System.out.println("Move disk " + n + " from rod " +  from_rod + " to rod " + to_rod); 
        towerOfHanoi(n-1, aux_rod, to_rod, from_rod); 
    } 
      
    //  Driver method 
    public static void main(String args[]) 
    { 
        int n = 4; // Number of disks 
        towerOfHanoi(n, \'A\', \'C\', \'B\');  // A, B and C are names of rods 
    } 
} 
```

