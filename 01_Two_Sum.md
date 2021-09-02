# 1. Two Sum
###### tags: `Leetcode` `DSA`
###### Difficulty: easy
### Description
>**Problem**
>Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
>
>You may assume that each input would have exactly one solution, and you may not use the same element twice.You can return the answer in any order.

>**Example**
>Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Because nums[0] + nums[1] == 9, we return [0, 1].

### Solution
* Brute Force  
Unaccepted due to Time Limit Exceeded.
```c
//Note: The returned array must be malloced, assume caller calls free().

int* twoSum(int* nums, int numsSize, int target, int* returnSize){
    int* arr = (int *)malloc(sizeof(int)*2);
    *returnSize = 2;
    
    for (int i = 0 ;i < numsSize ;i++ ){
        for (int j = i+1 ;j < numsSize ;j++ )
            if (*(nums+i) + *(nums+j) == target){ 
                arr[0] = i,arr[1] = j;
                return arr;  
            }
    }
    
    return arr;
}
```

Time complexity : O(n^2)
For each element, we try to find its complement by looping through the rest of array which takes O(n) time. Therefore, the time complexity is O(n^2).

Space complexity : O(1).
 

* Hash  
Accepted but it's only  faster than 9.11% of C online submissions.  
Further ,the memory usage is 6.6 MB, less than 6.10% submissons. 
```c
//Note: The returned array must be malloced, assume caller calls free().

#define Size 10000

int hash_function(int key){
    int ret = key % Size ;
    return ret < 0 ? ret+Size : ret ; 
}


int search(int* key_arr ,int* val_arr ,int key){
    int index = hash_function(key);
    while(val_arr[index]){
        if (key_arr[index] == key){
            return val_arr[index];
        }
        index++;
        index%=Size;
    } 
    return 0;    
}

void insert(int* key_arr ,int* val_arr ,int key ,int value){
    int index = hash_function(key);
    while(val_arr[index]){      //already exists
        index ++;               //place the element to next row
        index %= Size ; 
    }
    key_arr[index] = key;
    val_arr[index] = value;
    
}

int* twoSum(int* nums, int numsSize, int target, int* returnSize){
    int key_arr[Size];
    int val_arr[Size] = {0};
    *returnSize = 2;
    
    for(int i = 0 ; i < numsSize ;i++){
        int complement = target - nums[i];
        int ret = search(key_arr,val_arr,complement);
        if(ret){
            int* return_arr = (int*)malloc(sizeof(int)*2);
            return_arr[0] = i;
            return_arr[1] = ret-1;
            return return_arr;
        }
        //insert
        insert(key_arr,val_arr,nums[i],i+1);             
    }
    
    *returnSize = 0;
    return NULL;    
}
```

Time complexity : O(n). We traverse the list containing nn elements only once. Each look up in the table costs only O(1) time.

Space complexity : O(n). The extra space required depends on the number of items stored in the hash table, which stores at most n elements.
