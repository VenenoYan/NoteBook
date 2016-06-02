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
    
    vector<vector<int> > generate(int numRows) {
        vector<vector<int>> r(numRows);
        r.clear();

        for (int i = 0; i < numRows; i++) {
            r[i].resize(i + 1);
            r[i][0] = r[i][i] = 1;

            for (int j = 1; j < i; j++)
                r[i][j] = r[i - 1][j - 1] + r[i - 1][j];
        }

        return r;
    }
```

###Lesson
* 
操作前后先压入1.操作实现功能：从0到i-1，每个和后一个相加，然后压入。
* 
除了开始和最后一个，其余的都是肩上的两个数相加

##119. Pascal's Triangle II

Given an index k, return the kth row of the Pascal's triangle.

For example, given k = 3,
Return [1,3,3,1].

###Solution
```C
vector<int> getRow(int rowIndex) {
    vector<int> ret;
    vector<int> temp;
    ret.clear();
    temp.clear();
    ret.push_back(1);
    if(rowIndex==0)
        return ret;
    for(int i = 1;i<=rowIndex;++i)
    {
        temp.push_back(1);
        for(int j = 0;j<i;++j)
        {
            int kk = j+1<i?ret[j+1]:0;      //此处好好分析
            temp.push_back(ret[j]+kk);
        }
        ret = temp;
        temp.clear();
    }
    return ret;
}
```
###Lesson
* 
除了开始和最后一个，其余的都是肩上的两个数相加