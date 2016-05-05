
### 3Sum_Closest
Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution:<br>
求给定数组中任意三个数满足其和距离一个target最近。输出这三个数

    For example, given array S = {-1 2 1 -4}, and target = 1.
    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).



### Code

```C++
/*  common version
nums: array
num: the three fingers
diff: the first three divide target
sum: sum of three fingers
*/
void func1(vector<int> &nums,vector<int> &num,int target,int *diff,int *sum){
    for(vector<int>::iterator iter1=nums.begin();iter1!=(nums.end()-2);++iter1){
        for(vector<int>::iterator iter2=iter1+1;iter2!=(nums.end()-1);++iter2){
            for(vector<int>::iterator iter3=iter2+1;iter3!=nums.end();++iter3){
                if(abs(*iter1+*iter2+*iter3-target)<*diff){
                    *sum=*iter1+*iter2+*iter3;
                    *diff=abs(*iter1+*iter2+*iter3-target);
                    num.clear();
                    num.push_back(*iter1);
                    num.push_back(*iter2);
                    num.push_back(*iter3);
                }
            }
        }
    }
}

//better version
void func2(vector<int> &nums,vector<int> &num,int target,int *diff,int *sum){
    sort(nums.begin(),nums.end());
    vector<int>::iterator start,last;
    for(vector<int>::iterator iter1=nums.begin();iter1!=(nums.end());++iter1){
        start=iter1+1;
        last=nums.end()-1;
        while(start<last){
            if(abs(*iter1+*start+*last-target)<=*diff){
                *diff=abs(*iter1+*start+*last-target);
                *sum=*iter1+*start+*last;
                num.clear();
                num.push_back(*iter1);
                num.push_back(*start);
                num.push_back(*last);
                
            }
            if((*iter1+*start+*last)<=target){
                ++start;
                while(start<last&&*start==*(start-1)) ++start;
            }else{
                --last;
                while(start<last&&*last==*(last+1)) --last;
            }           //target is always immutable.So,sum>target, --last,otherwise ++start
        }
    }
}```


### Special cases:

```C++
int data1[]={-1,-1,1,1,3}      target =-1
vector<int> data2(10,0)       target=2
int data3[]={1,2,4,8,16,32,64,128}  target=82;```


### Lesson

* 
Special cases;
* 
target is immutable
* 
sort firstly with quick-sort

[返回目录](README.md)