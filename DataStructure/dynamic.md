#[动态规划](http://www.zhihu.com/question/23995189)
动态规划算法通常基于一个递推公式及一个或多个初始状态。 当前子问题的解将由上一次子问题的解推出。

分治算法是将问题划分成相对独立的子问题，递归的解决所有子问题，

动态规划是对于 某一类问题 的解决方法！！重点在于如何鉴定“某一类问题”是动态规划可解的而不是纠结解决方法是递归还是递推！

1.动态规划通常情况下应用于最优化问题，这类问题一般有很多个可行的解，每个解有一个值，而我们希望从中找到最优的答案。

2.该问题必须符合无后效性。即当前状态是历史的完全总结，过程的演变不再受此前各种状态及决策的影响。

一个问题是该用递推、贪心、搜索还是动态规划，完全是由这个问题本身阶段间状态的转移方式决定的！
但是贪心、动态规划是算法，而递推、分治是解决方式或者技巧
* 
每个阶段只有一个状态->递推；
* 
每个阶段的最优状态都是由上一个阶段的最优状态得到的->[贪心](http://blog.csdn.net/yelbosh/article/details/7649717)；
* 
把原问题拆分为多个子问题，然后递归地解决子问题-->分治
* 
每个阶段的最优状态是由之前所有阶段的状态的组合得到的->搜索；
* 
每个阶段的最优状态可以从之前某个阶段的某个或某些状态直接得到而不管之前这个状态是如何得到的->动态规划
    * 
一步一个脚印！

=====》动态规划是通过拆分问题，定义问题状态和状态之间的关系，使得问题能够以递推（或者说分治）的方式去解决。



自己理解：

贪心：每次选择能让当前状态距离问题最近的解，然后在次基础上继续！所以每次选择的不一定是最优解，但一定是跨步最大的（贪心嘛）。

动态规划：把问题分为子问题，找到状态转移方程。每一步都是为了最终最优解前进。每解决一步，就以当前为起点继续。不断把状态转移给下一个，直至最终达到最优。

[返回目录](README.md)