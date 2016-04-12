##图：
###1.实现：数组、邻接表、十字链表、邻接多重表
####1.1 数组实现
记录顶点，然后用邻接矩阵记录边的信息
####1.2 邻接表实现
```C
图的链式存储形式，对每个顶点都建立一个单链表。
表头节点：
    firstarc：指向第一个与该头部节点邻接的节点
    data: 必要的信息
内部节点：
    adjvex：顶点在图中的位置
    nextarc：下一个与该头节点邻接的顶点
    info：信息
然后这些单链表的表头节点按顺序存放，以便随即访问。
逆邻接表：即对每个对点建立一个以该顶点为头的弧的表
```
####1.3 十字链表实现
有向图的另一种链式存储方式
####1.4 邻接多重表实现
无向图的另一种链式存储方式

###2.遍历：对所有顶点扫描一次，故有一个辅助数组记录是否已访问
####2.1 BFS：广度优先搜索
类似于树的层次遍历

**思想：**
```
初始时，所有顶点未访问。BFS选择一个顶点开始访问，然后对该顶点进行层次遍历直至结束；
然后从这些邻接点出发继续访问他们的邻接点；
直至所以节点都被访问到。
```
**实现：**
```C
bool visited[num_of_vex]
void DFS_Traverse(Graph g,int v)
{
    for(v=0;v<num_of_vex;++v)   visited[v] = false;
    for(v=0;v<num_of_vex;++v)   
    {
        if(visited[v] == false)
            DFS(g,v);
    }   //以防还有未访问到的节点
}       
void DFS(Graph g,int v)
{
    visited[v] = true;
    for(w = firstadjvex(g,v);w>=0;w = nextadjvex(g,v,w))
        if(visited[v] == false) 
            DFS(g,w);
}   //深度遍历以该顶点为起始的路径
```
**总结：**
```C
数组实现：  O（n*n）    n代表顶点数
邻接表实现：O（n+e）    n代表顶点数，e代表边/弧数
```
####2.2 DFS：深度优先搜索
类似于树的先根遍历

**思想：**
```
初始时，所有顶点未访问。DFS选择一个顶点开始访问，然后从该顶点进行深度遍历直至结束或者遇到已访问的节点；
若此时还有未访问的节点，则以该节点开始继续；
直至所以节点都被访问到。
```
**实现：**
```C
bool visited[num_of_vex]
void DFS_Traverse(Graph g,int v)
{
    for(v=0;v<num_of_vex;++v)   visited[v] = false;
    for(v=0;v<num_of_vex;++v)   
    {
        if(visited[v] == false)
            DFS(g,v);
    }   //以防还有未访问到的节点
}       
void DFS(Graph g,int v)
{
    visited[v] = true;
    for(w = firstadjvex(g,v);w>=0;w = nextadjvex(g,v,w))
        if(visited[v] == false) 
            DFS(g,w);
}   //深度遍历以该顶点为起始的路径
```
**总结：**
```C
数组实现：  O（n*n）    n代表顶点数
邻接表实现：O（n+e）    n代表顶点数，e代表边/弧数
```



两点最短路径：图的遍历算法即可