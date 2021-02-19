Bubble sort

```java
public static void bubbleSort(int[] arr) {
    for (int i = 0; i < arr.length - 1; i++) {
        for (int j = 0; j < arr.length - 1 - i; j++) {
            if (arr[j] > arr[j + 1]) {
                // 如果左边的数大于右边的数，则交换，保证右边的数字最大
                arr[j + 1] = arr[j + 1] + arr[j];
                arr[j] = arr[j + 1] - arr[j];
                arr[j + 1] = arr[j + 1] - arr[j];
            }
        }
    }
}
```



select sort

```java
public static void selectionSort(int[] arr) {
    int minIndex;
    for (int i = 0; i < arr.length - 1; i++) {
        minIndex = i;
        for (int j = i + 1; j < arr.length; j++) {
            if (arr[minIndex] > arr[j]) {
                // 记录最小值的下标
                minIndex = j;
            }
        }
        // 将最小元素交换至首位
        int temp = arr[i];
        arr[i] = arr[minIndex];
        arr[minIndex] = temp;
    }
}
```



insert sort

```java
public static void insertSort(int[] arr) {
    // 从第二个数开始，往前插入数字
    for (int i = 1; i < arr.length; i++) {
        int currentNumber = arr[i];
        int j = i - 1;
        // 寻找插入位置的过程中，不断地将比 currentNumber 大的数字向后挪
        while (j >= 0 && currentNumber < arr[j]) {
            arr[j + 1] = arr[j];
            j--;
        }
        // 两种情况会跳出循环：1. 遇到一个小于或等于 currentNumber 的数字，跳出循环，currentNumber 就坐到它后面。
        // 2. 已经走到数列头部，仍然没有遇到小于或等于 currentNumber 的数字，也会跳出循环，此时 j 等于 -1，currentNumber 就坐到数列头部。
        arr[j + 1] = currentNumber;
    }
}
```

```java
public static void insertSort(int[] arr) {
    // 从第二个数开始，往前插入数字
    for (int i = 1; i < arr.length; i++) {
        // j 记录当前数字下标
        int j = i;
        // 当前数字比前一个数字小，则将当前数字与前一个数字交换
        while (j >= 1 && arr[j] < arr[j - 1]) {
            int temp = arr[j];
            arr[j] = arr[j - 1];
            arr[j - 1] = temp;
            // 更新当前数字下标
            j--;
        }
    }
}
```



shell sort

```java
public static void shellSort(int[] arr) {
    // 间隔序列，在希尔排序中我们称之为增量序列
    for (int gap = arr.length / 2; gap > 0; gap /= 2) {
        // 分组
        for (int groupStartIndex = 0; groupStartIndex < gap; groupStartIndex++) {
            // 插入排序
            for (int currentIndex = groupStartIndex + gap; currentIndex < arr.length; currentIndex += gap) {
                // currentNumber 站起来，开始找位置
                int currentNumber = arr[currentIndex];
                int preIndex = currentIndex - gap;
                while (preIndex >= groupStartIndex && currentNumber < arr[preIndex]) {
                    // 向后挪位置
                    arr[preIndex + gap] = arr[preIndex];
                    preIndex -= gap;
                }
                // currentNumber 找到了自己的位置，坐下
                arr[preIndex + gap] = currentNumber;
            }
        }
    }
}
```

```java
public static void shellSort(int[] arr) {
    // 间隔序列，在希尔排序中我们称之为增量序列
    for (int gap = arr.length / 2; gap > 0; gap /= 2) {
        // 从 gap 开始，按照顺序将每个元素依次向前插入自己所在的组
        for (int i = gap; i < arr.length; i++) {
            // currentNumber 站起来，开始找位置
            int currentNumber = arr[i];
            // 该组前一个数字的索引
            int preIndex = i - gap;
            while (preIndex >= 0 && currentNumber < arr[preIndex]) {
                // 向后挪位置
                arr[preIndex + gap] = arr[preIndex];
                preIndex -= gap;
            }
            // currentNumber 找到了自己的位置，坐下
            arr[preIndex + gap] = currentNumber;
        }
    }
}
```



heap sort

```java
public static void heapSort(int[] arr) {
    // 构建初始大顶堆
    buildMaxHeap(arr);
    for (int i = arr.length - 1; i > 0; i--) {
        // 将最大值放到数组最后
        exchange(arr, 0, i);
        // 调整剩余数组，使其满足大顶堆
        maxHeapify(arr, 0, i);
    }
}

// 构建初始大顶堆
public static void buildMaxHeap(int[] arr) {
    // 从最后一个非叶子结点开始调整大顶堆，最后一个非叶子结点的下标就是 arr.length / 2-1
    for (int i = arr.length / 2 - 1; i >= 0; i--) {
        maxHeapify(arr, i, arr.length);
    }
}

// 调整大顶堆，第三个参数表示剩余未排序的数字的数量，也就是剩余堆的大小
private static void maxHeapify(int[] arr, int i, int heapSize) {
    // 左子结点下标
    int l = 2 * i + 1;
    // 右子结点下标
    int r = l + 1;
    // 记录根结点、左子树结点、右子树结点三者中的最大值下标
    int largest = i;
    // 与左子树结点比较
    if (l < heapSize && arr[l] > arr[largest]) {
        largest = l;
    }
    // 与右子树结点比较
    if (r < heapSize && arr[r] > arr[largest]) {
        largest = r;
    }
    if (largest != i) {
        // 将最大值交换为根结点
        exchange(arr, i, largest);
        // 再次调整交换数字后的大顶堆
        maxHeapify(arr, largest, heapSize);
    }
}
// 交换元素
private static void exchange(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```



quick sort

```java
public static void quickSort(int[] arr) {
    quickSort(arr, 0, arr.length - 1);
}
public static void quickSort(int[] arr, int start, int end) {
    // 如果区域内的数字少于 2 个，退出递归
    if (start >= end) return;
    // 将数组分区，并获得中间值的下标
    int middle = partition(arr, start, end);
    // 对左边区域快速排序
    quickSort(arr, start, middle - 1);
    // 对右边区域快速排序
    quickSort(arr, middle + 1, end);
}
// 将 arr 从 start 到 end 分区，左边区域比基数小，右边区域比基数大，然后返回中间值的下标
public static int partition(int[] arr, int start, int end) {
    // 取第一个数为基数
    int pivot = arr[start];
    // 从第二个数开始分区
    int left = start + 1;
    // 右边界
    int right = end;
    // left、right 相遇时退出循环
    while (left < right) {
        // 找到第一个大于基数的位置
        while (left < right && arr[left] <= pivot) left++;
        // 交换这两个数，使得左边分区都小于或等于基数，右边分区大于或等于基数
        if (left != right) {
            exchange(arr, left, right);
            right--;
        }
    }
    // 如果 left 和 right 相等，单独比较 arr[right] 和 pivot
    if (left == right && arr[right] > pivot) right--;
    // 将基数和中间数交换
    if (right != start) exchange(arr, start, right);
    // 返回中间值的下标
    return right;
}
private static void exchange(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```



merge sort

```java
public static void quickSort(int[] arr) {
    quickSort(arr, 0, arr.length - 1);
}
public static void quickSort(int[] arr, int start, int end) {
    // 如果区域内的数字少于 2 个，退出递归
    if (start >= end) return;
    // 将数组分区，并获得中间值的下标
    int middle = partition(arr, start, end);
    // 对左边区域快速排序
    quickSort(arr, start, middle - 1);
    // 对右边区域快速排序
    quickSort(arr, middle + 1, end);
}
// 将 arr 从 start 到 end 分区，左边区域比基数小，右边区域比基数大，然后返回中间值的下标
public static int partition(int[] arr, int start, int end) {
    // 取第一个数为基数
    int pivot = arr[start];
    // 从第二个数开始分区
    int left = start + 1;
    // 右边界
    int right = end;
    // left、right 相遇时退出循环
    while (left < right) {
        // 找到第一个大于基数的位置
        while (left < right && arr[left] <= pivot) left++;
        // 交换这两个数，使得左边分区都小于或等于基数，右边分区大于或等于基数
        if (left != right) {
            exchange(arr, left, right);
            right--;
        }
    }
    // 如果 left 和 right 相等，单独比较 arr[right] 和 pivot
    if (left == right && arr[right] > pivot) right--;
    // 将基数和中间数交换
    if (right != start) exchange(arr, start, right);
    // 返回中间值的下标
    return right;
}
private static void exchange(int[] arr, int i, int j) {
    int temp = arr[i];
    arr[i] = arr[j];
    arr[j] = temp;
}
```

