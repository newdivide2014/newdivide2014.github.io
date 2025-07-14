# Leetcode 879.盈利问题

# 题目

难易程度： hard  
来源：力扣（LeetCode） 879.盈利问题  
[题目传送门](https://leetcode-cn.com/problems/profitable-schemes)

> 集团里有`n`名员工，他们可以完成各种各样的工作创造利润。  
> 第`i`种工作会产生`profit[i]`的利润，它要求`group[i]`名成员共同参与。如果成员参与了其中一项工作，就不能参与另一项工作。  
> 工作的任何至少产生`minProfit`利润的子集称为**盈利计划**。并且工作的成员总数最多为`n`。  
> 有多少种计划可以选择？因为答案很大，所以 返回结果模`10^9 + 7`的值。

```
示例：
输入：n = 5, minProfit = 3, group = [2,2], profit = [2,3]
输出：2
解释：至少产生 3 的利润，该集团可以完成工作 0 和工作 1 ，或仅完成工作 1 。
总的来说，有两种计划。
```

# 题解学习

这种一看就是动态规划，知道动态规划也写不出来呀，唉，看答案学吧。

```c
int profitableSchemes(int n, int minOrofit, int* group, int profit, int profitSize) {
    int len = groupSize, MOD = (int)1e9 + 7;
}
```



---

> : 嘟囔  
> URL: http://localhost:1313/zh/zh/posts/leetcode-879/  

