> 第一篇二分搜索论文是 1946 年发表，然而第一个没有 bug 的二分查找法却是在 1962 年才出现，中间用了 16 年的时间。

**书写二分查找法的重点，边界问题**
## 最基础的二分查找实现
```java
public static int binaryFind(int[] arr, int n) {
    int l = 0;
    int r = arr.length - 1;

    // [l, r]
    while (l <= r) {
        int mid = (l + r) / 2;
        if (arr[mid] == n) {
            return mid;
        } else if (arr[mid] > n) {
            r = mid - 1;
        } else {
            l = mid + 1;
        }
    }

    return -1;
}
```


## 关于二分查找的变种问题

### 查找第一个值等于给定值的元素
```java
public static int binaryFind(int[] arr, int val) {
    int l = 0;
    int r = arr.length - 1;

    // [l, r]
    while (l <= r) {
        int mid = (l + r) / 2;
        // --- 改动开始
        if (arr[mid] == val) {
            if(mid == 0 || arr[mid-1] != val)
                return mid;
            else 
                r = mid - 1;
        // --- 改动结束
        } else if (arr[mid] > val) {
            r = mid - 1;
        } else {
            l = mid + 1;
        }
    }

    return -1;
}
```

### 查找最后一个值等于给定值的元素

```java
public static int binaryFind(int[] arr, int val) {
    int l = 0;
    int r = arr.length - 1;

    // [l, r]
    while (l <= r) {
        int mid = (l + r) / 2;
        if (arr[mid] == val) {
            // --- 改动开启
            if (mid == arr.length - 1 || arr[mid + 1] != val)
                return mid;
            else
                l = mid + 1;
            // --- 改动结束
        } else if (arr[mid] > val) {
            r = mid - 1;
        } else {
            l = mid + 1;
        }
    }

    return -1;
}
```

### 查找第一个大于等于给定值的元素

```java
public static int binaryFind(int[] arr, int val) {
    int l = 0;
    int r = arr.length - 1;

    // [l, r]
    while (l <= r) {
        int mid = (l + r) / 2;
        if (arr[mid] >= val) {
            // --- 改动开启
            if (mid == 0 || arr[mid - 1] < val)
                return mid;
            else
                r = mid - 1;
            // --- 改动结束
        } else {
            l = mid + 1;
        }
    }

    return -1;
}
```

### 查找最后一个小于等于给定值的元素

```java
public static int binaryFind(int[] arr, int val) {
    int l = 0;
    int r = arr.length - 1;

    // [l, r]
    while (l <= r) {
        int mid = (l + r) / 2;
        if (arr[mid] <= val) {
            // --- 改动开启
            if (mid == arr.length - 1 || arr[mid + 1] > val)
                return mid;
            else
                r = mid - 1;
            // --- 改动结束
        } else {
            r = mid - 1;
        }
    }

    return -1;
}
```

## leetcode习题集
- [所有题目](https://leetcode-cn.com/tag/binary-search/problemset/)

**推荐的题目**
- []

## 二分查找的局限性
- 依赖数组存储数据
- 数组中数据有序
- 数据量太小不适合
- 数据量太大也不适合 因为要连续空间

## 总结
二分查找更加适合近似查找的问题上。比如以上4种变体。其他查找情况更加适合哈希表以及查找树。