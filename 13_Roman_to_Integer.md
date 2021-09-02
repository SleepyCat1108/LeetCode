# 13. Roman to Integer
###### tags: `Leetcode`
###### Difficulty: easy
### Description
>**Problem**
>Roman numerals are represented by seven different symbols: I, V, X, L, C, D and M.
>Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not IIII. Instead, the number four is written as IV.

>I can be placed before V (5) and X (10) to make 4 and 9. 
X can be placed before L (50) and C (100) to make 40 and 90. 
C can be placed before D (500) and M (1000) to make 400 and 900.


| Symbol| I | V | X | L | C  |  D |  M |
|-------|---|---|---|---|----|----|----|
| Value | 1 | 5 | 10| 50| 100| 500|1000|


>**Example**
Input: s = "IX"
Output: 9

>Input: s = "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.

### Solution
*C Solution*
Accepted and it’s faster than 55% of C online submissions.
However ,the memory usage is 6MB, less than 12.08% submissons.

```c
int calculate(unsigned int* arr ,char* s ){
    int total = 0;
    for(int i = 0 ;i < strlen(s) ;i++ ){
        if(arr[s[i]]<arr[s[i+1]])
            total = total - arr[s[i]];
        else
            total = total + arr[s[i]];
    }
    return total;
}

void Initailize_Array(unsigned int* array){
    array['I'] = 1;
    array['V'] = 5;
    array['X'] = 10;
    array['L'] = 50;
    array['C'] = 100;
    array['D'] = 500;
    array['M'] = 1000;
    array['\0']= 0;
}

int romanToInt(char * s){
    //acsii X == 88
    unsigned int Value_array[90] = {0};
    Initailize_Array(Value_array);
    int ret = calculate(Value_array,s);
    return ret;
}
```
