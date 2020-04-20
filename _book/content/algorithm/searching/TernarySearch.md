# Ternary Search

Like the binary search, it also separates the lists into sub-lists. This procedure divides the list into three parts using two intermediate mid values. As the lists are divided into more subdivisions, so it reduces the time to search a key value.

#### The complexity of Ternary Search Technique

1. Time Complexity: O(log3 n)
2. Space Complexity: O(1)

```java
int ternary_search(int l,int r, int x) {
    if(r >= l) {
        int mid1 = l + (r-l) / 3;
        int mid2 = r -  (r-l) / 3;
        if(ar[mid1] == x)
            return mid1;
        if(ar[mid2] == x)
            return mid2;
        if(x < ar[mid1])
            return ternary_search(l,mid1-1,x);
        else if(x > ar[mid2])
            return ternary_search(mid2+1,r,x);
        else
            return ternary_search(mid1+1,mid2-1,x);

    }
    return -1;
}
```

