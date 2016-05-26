##118. Pascal's Triangle 

Given numRows, generate the first numRows of Pascal's triangle.

```C
For example, given numRows = 5,
Return

[
     [1],
    [1,1],
   [1,2,1],
  [1,3,3,1],
 [1,4,6,4,1]
]```
###Solution
```C
    vector<vector<int>> generate(int numRows) {
        vector<vector<int>> ret;
        vector<int> line;
        vector<int> temp;
        line.clear();
        temp.clear();
        ret.clear();
        if(numRows==0)
            return ret;
        line.push_back(1);
        ret.push_back(line);
        for(int i = 1; i<numRows; ++i)
        {
            temp.push_back(1);
            for(int j = 0;j<i-1;++j)
                temp.push_back(line[j]+line[j+1]);
            temp.push_back(1);
            line.clear();
            swap(line,temp);
            ret.push_back(line);
        }
        return ret;
    }
```