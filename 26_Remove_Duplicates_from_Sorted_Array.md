# 26. Remove Duplicates from Sorted Array
###### tags: `Leetcode`
###### Difficulty: easy
### Description

>**Problem**
>Given an integer array nums sorted in non-decreasing order, remove the duplicates in-place such that each unique element appears only once. The relative order of the elements should be kept the same.
>
>Since it is impossible to change the length of the array in some languages, you must instead have the result be placed in the first part of the array nums. More formally, if there are k elements after removing the duplicates, then the first k elements of nums should hold the final result. It does not matter what you leave beyond the first k elements.
>
>Return k after placing the final result in the first k slots of nums.
>
>Do not allocate extra space for another array. You must do this by modifying the input array in-place with O(1) extra memory.

>**Example**
>1.
>Input: nums = [1,1,2]
Output: 2, nums = [1,2,_]
>2.
>Input: nums = [0,0,1,1,1,2,2,3,3,4]
Output: 5, nums = [0,1,2,3,4,_,_,_,_,_]



### Solution 
* Two Runner(Pointer)

Runtime: 12 ms, faster than 88.12% of C online submissions for Remove Duplicates from Sorted Array.  
Memory Usage: 7.7 MB, less than 24.40% of C online submissions for Remove Duplicates from Sorted Array.  

```c
int removeDuplicates(int* nums, int numsSize){
    int slow_runner = 0;
    int fast_runner = 1;
    
    if(numsSize == 0)
        return 0;
    if(numsSize == 1)
        return 1;
    
    for( ;fast_runner < numsSize ;fast_runner++){
        if(nums[slow_runner] != nums[fast_runner])   
            nums[++slow_runner] = nums[fast_runner];              
    }
    int array_length = slow_runner + 1;
    return array_length;
}
```
