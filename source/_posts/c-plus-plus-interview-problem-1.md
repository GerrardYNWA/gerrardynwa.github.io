title: C++ 面试题（一）
date: 2019-09-12 23:09:00
categories: Algorithm
tags: [interview problems]
---

　　C++常见面试题汇总——手撕算法

<!-- more -->

## 一、排序

　　LeetCode排序练习题——[912. Sort an array](https://leetcode.com/problems/sort-an-array/)

### 1. 快速排序

```C++
void quick_sort(vector<int>& nums, int l, int r) {
    if (l >= r) return;

    int i = l - 1, j = r + 1;
    int x = nums[l + ((r - l) >> 1)];
    while (i < j) {
        do {
            i++;
        } while (nums[i] > x);

        do {
            j--;
        } while (nums[j] < x);

        if (i < j) swap(nums[i], nums[j]);
    }

    quick_sort(nums, l, j);
    quick_sort(nums, j + 1, r);
}
```

### 2. 归并排序

```C++
void merge_sort(vector<int>& nums, vector<int>& tmp, int l, int r) {
    if (l >= r) return;

    int mid = l + ((r - l) >> 1);
    merge_sort(nums, tmp, l, mid);
    merge_sort(nums, tmp, mid + 1, r);

    int i = l, j = mid + 1;
    int k = 0;
    while (i <= mid && j <= r) {
        if (nums[i] <= nums[j]) {
            tmp[k++] = nums[i++];
        } else {
            tmp[k++] = nums[j++];
        }
    }

    while (i <= mid) tmp[k++] = nums[i++];
    while (j <= r) tmp[k++] = nums[j++];

    for (i = l, j = 0; i <= r; i++, j++) {
        nums[i] = tmp[j];
    }
}
```

### 3. 堆排序

```C++
void heapify(vector<int>& nums, int n, int i) {
    if (i >= n) return;

    int l = 2 * i + 1;
    int r = 2 * i + 2;
    int max = i;

    if (l < n && nums[l] > nums[max]) {
        max = l;
    }

    if (r < n && nums[r] > nums[max]) {
        max = r;
    }

    if (max != i) {
        swap(nums[max], nums[i]);
        heapify(nums, n, max);
    }
}

void build_heap(vector<int>& nums, int n) {
    int last_node = n - 1;
    int parent_node = (last_node - 1) / 2;
    for (int i = parent_node; i >= 0; i--) {
        heapify(nums, n, i);
    }
}

void heap_sort(vector<int>& nums, int n) {
    build_heap(nums, n);

    for (int i = n - 1; i >= 0; i--) {
        swap(nums[i], nums[0]);
        heapify(nums, i, 0);
    }
}
```

## 二、链表

### 1. 链表反转

### 2. 链表环及入口

