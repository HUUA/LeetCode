## 不同的二叉搜索树 2

### 题目描述

```
给定一个整数 n，生成所有由 1 ... n 为节点所组成的二叉搜索树。
示例:

输入: 3
输出:
[
  [1,null,3,2],
  [3,2,null,1],
  [3,1,null,null,2],
  [2,1,3],
  [1,null,2,null,3]
]
解释:
以上的输出对应以下 5 种不同结构的二叉搜索树：

   1         3     3      2      1
    \       /     /      / \      \
     3     2     1      1   3      2
    /     /       \                 \
   2     1         2                 3

```

### 分析

```
这是一到动态规划的项目，以其中一个点为根节点，得到左子树根节点的集合和右子树根节点的集合，
然后组合起来就是结果。
```

### 代码

```c++
vector<TreeNode*> creatTree(int start,int end){
        vector<TreeNode*> res;
        if(start>end){
            res.push_back(NULL);
            return res;
        }
        if(start==end){
            TreeNode* node=new TreeNode(start);
            res.push_back(node);
            return res;
        }
        for(int i=start;i<=end;i++){
            vector<TreeNode*> left=creatTree(start,i-1);
            vector<TreeNode*> right=creatTree(i+1,end);
            for(int j=0;j<left.size();j++){
                for(int k=0;k<right.size();k++){
                    TreeNode *node=new TreeNode(i);
                    node->left=left[j];
                    node->right=right[k];
                    res.push_back(node);
                }
            }
        }
        return res;
    }
    vector<TreeNode*> generateTrees(int n) {
        vector<TreeNode*> res;
        if(n<1) return res;
        res=creatTree(1,n);
        return res;
    }
```

