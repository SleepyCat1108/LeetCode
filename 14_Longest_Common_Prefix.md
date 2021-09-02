# 14. Longest Common Prefix
###### tags: `Leetcode`
###### Difficulty: easy
### Description

>**Problem**
>Write a function to find the longest common prefix string amongst an array of strings.
>If there is no common prefix, return an empty string "".

>**Example**
>*Ex1*:
Input: strs = ["flower","flow","flight"]
Output: "fl"
*Ex2*:
Input: strs = ["dog","racecar","car"]
Output: ""


### Solution 1 
* Horizontal scanning

For a start we will describe a simple way of finding the longest prefix shared by a set of strings LCP(S1…Sn). We will use the observation that : LCP(S1…Sn) = LCP(LCP(LCP(S1, S2),S3),…Sn)

To employ this idea, the algorithm iterates through the strings [S1…Sn] finding at each iteration i the longest common prefix of strings LCP(S1…Si).When LCP(S1…Si) is an empty string, the algorithm ends. Otherwise after n iterations, the algorithm returns LCP(S1…Sn).


Runtime: 4 ms, faster than 47.43% of C online submissions.  
Memory Usage: 5.8 MB, less than 96.82% of C online submissions.

```c
char* longestCommonPrefix(char** strs, int strsSize){
    int str_len = strlen(*strs);
    char* common = (char*)malloc(sizeof(char)*(str_len+1));  //sizeof(char) == 1
    common = *strs;
    common[str_len] = '\0';
    
    for(int i = 1 ; i < strsSize ;i++ ){
        int str_len_cmp = strlen(strs[i]);
        for(int j = 0 ;j <= str_len_cmp && j < str_len ;j++ ){
            if( common[j] != strs[i][j] || strs[i][j] == '\0')
                common[j] = '\0';
        }       
    }   
    return common;
}
```
### Complexity Analysis
* Time complexity : O(S) 

S is the sum of all characters in all strings, the worst case all n strings are the same.
The algorithm compares the string S1 with the other strings [S2 …Sn]. There are S character comparisons, where S is the sum of all characters in the input array.
* Space complexity : O(1)

We only used constant extra space.


### Solution 2
* Divide and Conquer

The idea of the algorithm comes from the associative property of LCP operation.We notice that : LCP(S1 ... Sn) = LCP(LCP(S1 ... Sk), LCP (Sk+1 ... Sn))

we use divide and conquer technique, where we split the LCP(Si ... Sj) problem into two subproblems LCP(Si ... Smid) and LCP(Smid+1 ... Sj)where mid is (i + j)/2
We use their solutions lcpLeft and lcpRight to construct the solution of the main problem LCP.

Runtime: 0 ms, faster than 100.00% of C online submissions.  
Memory Usage: 6 MB, less than 35.18% of C online submissions.
```c
int check_common_char(int len1,int len2,char* left,char* right){
    int i = 0;
    for(;i < len1 && i < len2 ;i++ ){
        if (left[i] != right[i])
            break;
    }
    return i;
}


int prefix_len(char** strs,int size){   
    
    if (size == 1)
        return strlen(strs[0]);
    
    int mid = size>>1;      //using shift instead of division operand
    int len1 = prefix_len(strs,mid);    
    int len2 = prefix_len(strs+mid,size-mid);    
    int common_len = check_common_char(len1,len2,*strs,*(strs+mid));
    
    return common_len;
}


char* longestCommonPrefix(char** strs, int strsSize){
    if (strsSize == 0)
        return "";
    int len = prefix_len(strs,strsSize);    
    strs[0][len] = '\0';
    return strs[0];
}

```
### Complexity Analysis 
> 致謝  劉宇峻

* Time Complexity：
Worst Case :
$$
T(n) = 2 T(n/2) + O(m)
$$

$$
T(n) = 2 ( 2 T(n/4) + O(m)) + O(m)
$$

$$
T(n) = O(m) + 2 O(m) + 4 O(m) + ... 2^k O(m) \quad where \ k = log_2 n
$$

$$
T(n) = \frac{1-2^k}{1-2} O(m)
= (n - 1) O(m) = O(nm)
$$

Best Case :
$$
m = \{ m_1, m_2, m_3, ...,m_n \}
$$

$$
O(mn) \rightarrow O(\sum_i m_i)
$$

$$
O(\sum_i m_i) \geq O(n\min_i m_i) = O(nm_{min})
$$

* Space Complexity：
The maximum number of function stored in stack is $log_2 n$, every function store up to m characters. Therefore, the space complexity is 

$O(mlog_2 n)$   (For the case return value of prefix_len is of type char*) 

$O(log_2 n)$   (For the case return value of prefix_len is of type int)




### Solution 3
* Binary Search with Vertical Scan
    
Each time search space is divided in two equal parts, one of them is discarded, because it is sure that it doesn't contain the solution. There are two possible cases:

S[1...mid] is not a common string.
This means that for each j > i S[1..j] is not a common string and we discard the second half of the search space.
S[1...mid] is a common string.
This means that for for each i < j S[1..i] is a common string and we discard the first half of the search space, because we try to find longer common prefix.

Runtime: 4 ms, faster than 43.30% of C online submissions for Longest Common Prefix.  
Memory Usage: 6 MB, less than 35.01% of C online submissions for Longest Common Prefix.

``` c
int common_len = 0;

int BinarySearch(char** strs ,int strsSize ,int start ,int mid){   
    bool discard_half = false;
    int string_len = strlen(strs[0]);
    
    for(int j = start ; j < mid+1 ;j++ ){
        for(int i = 1 ;i < strsSize ;i++ ){
            if(strs[0][j] != strs[i][j]){
                common_len = j;
                j = mid+1;                  //break the outer loop
                discard_half = true;  
                break;
            }    
        }
    }
    
    if(!discard_half){
        start = mid+1;
        mid = (mid + string_len) >> 1;
        
        if (start == string_len)
            return string_len;
    
        if (mid != string_len){
            common_len = BinarySearch(strs,strsSize,start,mid);
            return common_len;
        }  
    }   
    return common_len;
}

char* longestCommonPrefix(char** strs, int strsSize){   
    if(strcmp(strs[0],"") == 0)
        return "";    // "" means a string with size == 1 , the element is '\0'
    if (strsSize == 1)
        return strs[0];
    
    int len = strlen(strs[0]);
    int mid   = len/2;
    int start = 0;
   
    common_len = BinarySearch(strs,strsSize,start,mid);
    strs[0][common_len] = '\0';
    return strs[0];
    
}

```

### Complexity Analysis 
