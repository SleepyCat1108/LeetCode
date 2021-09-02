# 9. Palindrome Number
###### tags: `Leetcode`
###### Difficulty: easy
### Description
>**Problem**
>Given an integer x, return true if x is palindrome integer.
>
>An integer is a palindrome when it reads the same backward as forward. For example, 121 is palindrome while 123 is not.

>**Example**
Input: x = -121
Output: false
Explanation: From left to right, it reads -121. From right to left, it becomes 121-. Therefore it is not a palindrome.

### Solution
* First Attemp  
Accepted and it’s faster than 72.15% of C online submissions.  
However ,the memory usage is  6.1MB, less than 30.37% submissons.

```c
bool isPalindrome(int x){
    int count = 1;
    int n = x;
    
    if (x < 0)
        return false;
    
    while(n != 0){
        n = n/10;
        count ++; 
    }
    
    char ch[count+1];
    sprintf(ch,"%d",x);
    int begin_index = 0;
    int end_index   = strlen(ch) - 1;
  
    while(begin_index != end_index && end_index > begin_index){        
        if(ch[begin_index] == ch[end_index]){
            begin_index++;
            end_index--;
        }
        else
            return false;       
    }
    return true;   
}
```
* Second Attemp  
Accepted ,it beat 26.27% of C online submissions ,which is not good.  
But its memory usage 5.8MB, less than 94.92% of C online submissions.

We first calculate the range of int32 : -2,147,483,648 to 2,147,483,647.  
From the result ,we create a char array of size 12,and replace the *endindex* with *len-1-len*.
```c
bool isPalindrome(int x){
    if (x < 0)
        return false;
    
    char ch[12];
    int len = sprintf(ch,"%d",x);
    int index = 0;
    for(int index = 0 ;index < len/2 ;index++){
        if(ch[index] != ch[len-1-index])
            return false;     
    }
    return true;
    
}
```
