#### Bubble sort

Leetcode  75. Sort Colors

```java
class Solution {
    public void sortColors(int[] nums) {
        // worst O(n^2), best O(n), space O(1)    
        boolean numberSwitched;
        do {
            numberSwitched = false;
            for (int i = 0; i < nums.length -1; i++) {
                if (nums[i+1] < nums[i]) {
                    int tmp = nums[i+1];
                    nums[i+1] = nums[i];
                    nums[i] = tmp;
                    numberSwitched = true;
                }
            }
        } while (numberSwitched);
    }
}
```



#### Insertion Sort

template:

```java
public static List<Integer> insertSort(final List<Integer> numbers) {
    
   		// worst O(n^2), best O(n), space O(n)
    	// ArrayList is not good at insertion    
    	final List<Integer> sortedList = new LinkedList<>();
        
    	// outer loop label
        orignialList : for (Integer number : numbers) {
            for (int i = 0; i < sortedList.size(); i++) {
                if (number < sortedList.get(i)) {
                    sortedList.add(i, number);
                    continue orignialList;
                }
            }
            
            sortedList.add(sortedList.size(), number);
        }
        
        return sortedList;
        
    }
```



Leetcode 147. Insertion Sort List

```java
class Solution {
    public ListNode insertionSortList(ListNode head) {
    
        if (head == null)
            return head;
        
        ListNode dummy = new ListNode(0);
        
        while (head != null) {
            ListNode node = dummy;
            
            while(node.next != null && node.next.val < head.val) {
                node = node.next;
            }
                          
            ListNode tmp = head.next;
            head.next = node.next;
            node.next = head;
            head = tmp;
        }
        
        return dummy.next;
    }
}
```



Leetcode 406. Queue Reconstruction by Height

```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        
        // 将身高从高到低排序后依次插入即可
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
        
        // people: [[7,0],[7,1],[6,1],[5,0],[5,2],[4,4]]
        
        List<int[]> res = new LinkedList<>();
        
        // 对于某个人[h,k]来说，插入答案的第k位。
        for (int[] p : people) {
            res.add(p[1], p);
        }
        
        return res.toArray(new int[people.length][]);
    }
}
```



#### Quick Sort (sort in partition)

template

```java
public static List<Integer> quickSort(List<Integer> numbers) {
        if (numbers.size() < 2) {
            return numbers;
        }
        
    	// average O(nlogn), worst O(n^2)
        final Integer pivot = numbers.get(0);
        final List<Integer> lower = new ArrayList<>();
        final List<Integer> higher = new ArrayList<>();
        
        for (int i = 1; i < numbers.size(); i++) {
            if (numbers.get(i) < pivot) {
                lower.add(numbers.get(i));
            } else {
                higher.add(numbers.get(i));
            }
        }
        
        final List<Integer> sorted = quickSort(lower);
        sorted.add(pivot);
        sorted.addAll(quickSort(higher));
        
        return sorted;
    }
```





Leetcode 215. Kth Largest Element in an Array

```java
class Solution {
    public int findKthLargest(int[] nums, int k) {
        return quickSort(nums, 0, nums.length -1, k);
    }
    
    private int quickSort(int[] nums, int left, int right, int k) {
        if (left <= right) {
            int p = partition(nums, left, right);
            if (p == nums.length -k) {
                return nums[p];
            } else if (p > nums.length - k) {
                return quickSort(nums, left, p -1, k);
            } else {
                return quickSort(nums, p + 1, right, k);
            }
        }
        
        return -1;
    }
    
    private int partition(int[] nums, int left, int right) {
        // pick the first one as pivot
        int i = left + 1, j = right; 
        
        while(true) {
            while(i <= right && nums[i] < nums[left]) {
                i++;
            }
            
            while(j >= left + 1 && nums[j] > nums[left]) {
                j--;
            }
            
            if (i > j)
                break;
            
            int temp = nums[i];
            nums[i] = nums[j];
            nums[j] = temp;
            i++;
            j--;
        }
        
        int temp = nums[left];
        nums[left] = nums[j];
        nums[j] = temp;
        
        return j;
    }
}
```



#### Merge Sort (sort in merge)

template:

```java
public static List<Integer> mergeSort(List<Integer> numbers) {
        if (numbers.size() < 2) {
            return numbers;
        }
        // O(nlogn)
    	// (inclusive, exclusive)
        final List<Integer> leftHalf = numbers.subList(0, numbers.size()/2);
        final List<Integer> rightHalf = numbers.subList(numbers.size()/2, numbers.size());
        
        return merge(mergeSort(leftHalf), mergeSort(rightHalf));
    }
    
    public static List<Integer> merge(final List<Integer> left, final List<Integer> right) {
        int leftPtr = 0;
        int rightPtr = 0;
        
        final List<Integer> merged = new ArrayList<>(left.size() + right.size());
        
        while (leftPtr < left.size() && rightPtr < right.size()) {
            if (left.get(leftPtr) < right.get(rightPtr)) {
                merged.add(left.get(leftPtr));
                leftPtr++;
            } else {
                merged.add(right.get(rightPtr));
                rightPtr++;
            }
        }
        
        while (leftPtr < left.size()) {
            merged.add(left.get(leftPtr));
            leftPtr++;
        }
        
        while (rightPtr < right.size()) {
            merged.add(right.get(rightPtr));
            rightPtr++;
        }
        
        return merged;
    }
```



Leetcode 912.Sort an Array

```java
class Solution {
    public List<Integer> sortArray(int[] nums) {

        List<Integer> list = new ArrayList<>();
        int[] res = merge_sort(nums);
        for (int x : res) {
            list.add(x);
        }

        return list;
    }

    private int[] merge_sort(int[] nums) {
        if (nums.length <= 1)
            return nums;

        int pivot = nums.length / 2;
        int[] left_list = merge_sort(Arrays.copyOfRange(nums, 0, pivot));
        int[] right_list = merge_sort(Arrays.copyOfRange(nums, pivot, nums.length));
        return merge(left_list, right_list);
    }

    private int[] merge(int[] left_list, int[] right_list) {
        int[] ret = new int[left_list.length + right_list.length];
        int left_cursor = 0, right_cursor = 0, ret_cursor = 0;

        while (left_cursor < left_list.length && right_cursor < right_list.length) {
            if (left_list[left_cursor] < right_list[right_cursor]) {
                ret[ret_cursor++] = left_list[left_cursor++];
            } else {
                ret[ret_cursor++] = right_list[right_cursor++];
            }
        }

        while (left_cursor < left_list.length) {
            ret[ret_cursor++] = left_list[left_cursor++];
        }

        while (right_cursor < right_list.length) {
            ret[ret_cursor++] = right_list[right_cursor++];
        }
        return ret;
    }
}
```

