# 35. Search Insert Position
###### tags: `Leetcode`
###### Difficulty: easy
### Description

>**Problem**
Given a sorted array of distinct integers and a target value, return the index if the target is found. If not, return the index where it would be if it were inserted in order.
>*You must write an algorithm with O(log n) runtime complexity.*

 
>**Example**
>1.
>Input: nums = [1,3,5,6] , target = 5
Output: 2
>2.
>Input: nums = [1,3,5,6] , target = 2
Output: 1
>3.
>Input: nums = [1,3,5,6], target = 7
Output: 4
>4.
>Input: nums = [1,3,5,6], target = 0
Output: 0


### Solution
* Binary Search (Iterative)

Runtime: 13 ms, faster than 6.21% of C online submissions for Search Insert Position.   
Memory Usage: 5.8 MB, less than 99.61% of C online submissions for Search Insert Position.   

```c 
int searchInsert(int* nums, int numsSize, int target){
    int left = 0;
    int right= numsSize - 1;
    int mid  = 0;
    while(left <= right){
        mid = (left + right) >> 1;
        if(nums[mid] == target)
            return mid;
        else if(nums[mid] < target )
            left = mid+1;
        else 
            right= mid-1;
    }
    return left;
}
```

* Binary Search (Recursive)

Runtime: 4 ms, faster than 87.11% of C online submissions for Search Insert Position.   
Memory Usage: 6.1 MB, less than 41.12% of C online submissions for Search Insert Position.  

```c
int searchInsert(int* nums, int numsSize, int target){   
    int index = binary_search(nums ,0 ,numsSize-1 ,target);
    return index;  
}

int binary_search(int* nums ,int left ,int right ,int target){
    if(left > right)
        return left;   
    int mid = (left+right) >> 1;
    if(nums[mid] == target)
        return mid;
    else if(nums[mid] > target)
        return binary_search(nums ,left  ,mid-1 ,target);
    else   
        return binary_search(nums ,mid+1 ,right ,target);         
}
```
