## 二叉树的最大深度

### 题目描述

```
给定一个二叉树，找出其最大深度。
二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。
说明: 叶子节点是指没有子节点的节点。
示例：
给定二叉树 [3,9,20,null,null,15,7]，
    3
   / \
  9  20
    /  \
   15   7
返回它的最大深度 3 。
```

### 分析

```
分别计算出左子树和右子树的深度，比较这两个深度，取最大值 k。那么当前这棵树深度的最大值为k + 1
```

### 递归解法

```c++
int maxDepth(TreeNode* root) {
    if(root == NULL)  return 0;
    return max(maxDepth(root->left), maxDepth(root->right)) + 1;
}
```

###  迭代解法

```
用层序遍历。每遍历一层，就深度加1
```

```c++
int maxDepth(TreeNode* root) {
        if (!root) return 0; //判断为空条件
        int res = 0; //定义哨兵
        queue<TreeNode*> q{{root}}; //定义一个队列并初始化为root
        while (!q.empty()) { //循环条件是队列不为空
            ++res; //每经过一层，哨兵自增
            for (int i = q.size(); i > 0; --i) { //二叉树遍历
                TreeNode *t = q.front(); q.pop(); //出队列
                if (t->left) q.push(t->left); //如果左子树存在继续往左
                if (t->right) q.push(t->right); //如果右子树存在继续往右
            }
        }
        return res; //返回数值
    }
```

