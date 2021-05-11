```java
// Array definition
final int[] integers = new int[3];
final boolean[] bools = {false, true, true, false};
final String[] strings = new String[]{"one", "two"};
```



#### public static void sort(int[] arr, int from_Index, int to_Index)



Parameters:

arr: the array to be sorted

from_index: the index of the first element, ***inclusive***

to_index: the index of the last element, ***exclusive***



Return:

This method does not return any value;

e.g., 

```java
Arrays.sort(arr); // default, ascending order
Arrays.sort(arr, 1, 5) // sort subarray from arr[1] to arr[4]
Arrays.sort(arr, Collections.reverseOrder()) // decending order

// b a
Arrays.sort(arr, (a,b)-> b - a); // customized comparator, reverse order

arr should be type Integer instead of int
```

```java
# sort a two dimension array
    
    // first element decreasing, second element increasing
	Arrays.sort(people, (new Comparator<int[]>() {
        @Override
        public int compare(int[] o1, int[] o2) {
            if (o1[0] == o2[0]) {
                return o1[1] - o2[1];
            } else {
                return o2[0] - o1[0];
            }
        }
    }));
```



```java
public void customSorting() {
    final List<Integer> numbers = Arrays.asList(4,7,1,6,3,5,4);
    final List<Integer> expected = Arrays.asList(7,6,5,4,4,3,1);
    
    Collections.sort(numbers, new ReverseNumberOrder());
    assertEquals(expected, numbers);
}

public class ReverseNumberOrder implements Comparator<Integer> {
    @Override
    public int compare(Integer o1, Integer o2) {
        return o2 - o1;
    }
}
```



#### Array Sort

First element large -> small, second element small -> large

```java
Arrays.sort(people, (new Comparator<int[]>() {
    @Override
    public int compare(int[] o1, int[] o2) {
        if (o1[0] == o2[0]) {
            return o1[1] - o2[1]; // increasing
        } else {
            return o2[0] - o1[0]; // decreasing
        }
    }
}));
```



