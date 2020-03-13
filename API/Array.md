#### public static void sort(int[] arr, int from_Index, int to_Index)



Parameters:

arr: the array to be sorted

from_index: the index of the first element, ***inclusive***

to_index: the index of the last element, ***exclusive***



Return:

This method does not return any value;

e.g., 

```java
Arrays.sort(arr); // ascending order
Arrays.sort(arr, 1, 5) // sort subarray from arr[1] to arr[4]
Arrays.sort(arr, Collections.reverseOrder()) // decending order
  
Arrays.sort(arr, (a,b)-> b - a); // customized comparator, reverse order
```

-----
