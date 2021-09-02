# 20. Valid Parentheses
###### tags: `Leetcode`
###### Difficulty: easy
### Description

>**Problem**
Given a string s containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

>An input string is valid if:
Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.

>**Example**
Input: s = "()[]{}"
Output: true
>
>Input: s = "(]"
Output: false


Runtime:3 ms, faster than 15.67% of C online submissions for Valid Parentheses.  
Memory Usage: 5.5 MB, less than 99.44% of C online submissions for Valid Parentheses.


```c 
bool isValid(char * s){
    int string_len = strlen(s);
    char stack[string_len+1]; 
    int top = 1,last  = 0;
    stack[last] = 's';stack[string_len] = '\0';
    
    if (string_len %2 == 1)
        return false;
    
    /*Every if statement in the following for loop  accomplish 
    either push() or pop() ,and thus they all have  
    continue or return statement indicating either push() or pop() 
    has been done.*/ 
    
    for (int i = 0 ;i < string_len ;i++ ){            
        if (s[i] == '(' || s[i] == '[' || s[i] == '{'){        
            stack[top] = s[i];           
            last = top;
            top++;  
            continue;       //<--- Pay attention not to forget the "continue"
        }
        
        if (s[i] == ')' && stack[last] == '('){   
            top = last;
            last--;        
            continue;
        }        
        if (s[i] == ')' && stack[last] != '(')
            return false;
            
        if (s[i] == ']' && stack[last] == '['){  
            top = last;
            last--;    
            continue;
        }
        if (s[i] == ']' && stack[last] != '[' )
            return false;  
            
        if (s[i] == '}' && stack[last] == '{'){
            top = last;
            last--;
            continue;  
        }
        if (s[i] == '}' && stack[last] != '{' )
            return false;                   
    }   
    
    if(top == 1)
        return true;
    else 
        return false;
}

```
To write the code more concisely,here is another way using realloc based dynamic array.
```c
bool isValid(char * s){
    int stacksize = 0;
    char* stack = NULL,top;
    while(*s){       
        if (*s == '(' || *s == '[' || *s == '{'){
            ++stacksize;
            stack = (char*)realloc(stack,stacksize*sizeof(char));
            stack[stacksize-1] = *s++;
            continue;
        }
        
        if (stacksize == 0) 
            return false;
        top = stack[stacksize - 1];
        
        switch(*s){
            case ')': 
                if (top != '(')
                    return false;
                break;
            case ']':
                if (top != '[')
                    return false;
                break;
            case '}':
                if (top != '{')
                    return false;
                break;
        }
        stacksize--;
        stack = (char*)realloc(stack,stacksize*sizeof(char));
        s++;
        
    }
    return stacksize == 0;
}

```
