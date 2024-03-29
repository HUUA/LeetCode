## 不同的二叉搜索树

### 题目描述

```
给定一个整数 n，求以 1 ... n 为节点组成的二叉搜索树有多少种？
示例:

输入: 3
输出: 5
解释:
给定 n = 3, 一共有 5 种不同结构的二叉搜索树:

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3
```

### 二叉搜索树的性质

```
- 若任意节点的左子树不空，则左子树上所有节点的值均小于它的根节点的值
- 若任意节点的右子树不空，则右子树上所有节点的值均大于它的根节点的值
- 任意节点的左、右子树也分别为二叉搜索树
- 没有键值相等的节点
```

### 分析

```
给定i(1≤i≤n),由1...i组成的不同的二叉查找树有f(i)种，对于i以k(1≤k≤i)作为根节点左子树的节点为1,...,k−1共有k−1个节点，右子树的节点为k+1,...,i共有i−k个节点，然后左子树的组合数*右子树的组合数即为以k(1≤k≤i)作为根节点时的树的组合数量，把所有组合数量累加即为f(i)的值，又叫卡特兰数。
```

### 优化

```
- 当动态规划中存在成对的二叉搜索树子树镜像出现时，可以优化计算；
比如i = 4 时，f(4) = f(0)*f(3) +  f(1)*f(2) + f(2)*f(1) + f(3)*f(0)
- f(0)*f(3) 与 f(3)*f(0) 虽然在意义上不一样，但是在数值的结果上是一样的， 所以简化为 f(4) = ( f(0)*f(3) + f(1)*f(2) ) * 2
```

### 代码

```c++
int numTrees(int n) {
        vector<int> res(n+1,0); //定义一个数组，大小n+1，初始化0
        res[0] = 1; //首元素设置为1
        
        for (int i = 1; i <= n; ++i) { // 外循环
            for (int j = i-1; j >= i/2; --j) { //内循环
                
                if (i%2==1 && j == i/2) //区分左右子树以及优化
                    res[i] += res[j] * res[i-j-1]; //装态转移方程
                else
                    res[i] += res[j] * res[i-j-1]*2; //状态转移方程
            }
        }
        return res[n];
    }
```

