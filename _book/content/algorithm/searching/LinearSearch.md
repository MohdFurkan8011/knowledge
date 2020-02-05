# Linear Search

Linear searching techniques are the simplest technique. In this technique, the items are searched one by one. This procedure is also applicable for unsorted data set. Linear search is also known as sequential search. It is named as linear because its time complexity is of the order of n O(n).

#### The complexity of Linear Search Technique

1. **Time Complexity:** O(n)
2. **Space Complexity:** O(1)

```java
class GFG {  
	public static int search(int arr[], int x) { 
    	int n = arr.length; 
    	for(int i = 0; i < n; i++) { 
        	if(arr[i] == x) 
            	return i; 
    	} 
    	return -1; 
	} 
  
	public static void main(String args[]) { 
    	int arr[] = { 2, 3, 4, 10, 40 };  
    	int x = 10; 
      
    	int result = search(arr, x); 
    	if(result == -1) 
        	System.out.print("Element is not present in array"); 
    	else
        	System.out.print("Element is present at index " + result); 
	} 
} 
```