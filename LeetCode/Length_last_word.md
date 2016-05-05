
## Length of Last Word


Given a string s consists of upper/lower-case alphabets and empty space characters ' ', return the length of last word in the string.
If the last word does not exist, return 0.<br>
最后一个单词的长度<br>
Note: A word is defined as a character sequence consists of non-space characters only.

```C++
For example, 
Given s = "Hello World",
return 5.```


## Code

```C++
int lengthOfLastWord(string s){
    stack<char> space;
    size_t i,j,k;

    i=s.length()-1;

    while(i!=-1&&s[i]==' '){
        --i;
    }
    if(i==-1) 
        return 0;
    k=j=i;
    while(j!=-1&&s[j]!=' '){
        space.push(s[j]);
        --j;
    }
    return j==-1?space.size():k-j;
}```


## Special cases:

```C++
string s="Compare two blocks of memory";
string s1="h";
string s2="year  "```

## Lesson

* 
the use of stack
* 
indice problem

