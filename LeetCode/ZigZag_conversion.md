
## ZigZag Conversion

 The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)<br>
 竖着的Z字编码

```C
P   A   H   N
A P L S I I G
Y   I   R```

And then read line by line: "PAHNAPLSIIGYIR"
 Write the code that will take a string and make this conversion given a number of rows:

```C++
string convert(string text, int nRows);

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR". ```

## Code:

```C++
string convert(string s, int numRows){
    string ret="";
    int span,j;
    if(numRows==1)
        return s;
    for(int i=0;i<numRows;++i){
        span=2*i;
        j=i;
        while(j<s.size()){
            ret+=s[j];
            if(span==0||span==2*(numRows-1))
                span=2*(numRows-1);
            else
                span=2*(numRows-1)-span;
            j+=span;
        }
        ret+="\n";
    }
    cout<<ret<<endl;

    return ret;
}```

## Special cases:

* 
convert("h",1);
* 
convert("JKLHJUI",4);

## Lesson:

* 
return s if numRows==1
* 
span
