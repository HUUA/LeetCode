## AVL树

### 题目描述

```
给定一个二叉树，判断它是否是高度平衡的二叉树。
本题中，一棵高度平衡二叉树定义为：
一个二叉树每个节点 的左右两个子树的高度差的绝对值不超过 1。
示例 1:
给定二叉树 [3,9,20,null,null,15,7]
    3
   / \
  9  20
    /  \
   15   7
返回 true。
```

### 分析

```
对每一个节点（即每一颗子树），求它的左子树的高度和右子树的高度，然后判断高度差是否超过一。
历遍所有的子树，即可达到判断结果。
```

### 代码

```c++
bool isBalanced(TreeNode* root) {
        if(!root) return true;//如果是空，那么树是平衡树，同时这一条语句保证下面的指针是有效的
        if(abs(depth(root->left)-depth(root->right))>1)return false;//不满足，false
        return isBalanced(root->left)&&isBalanced(root->right);//继续历遍整颗树
    }
    int depth(TreeNode* root)//计算树的高度
    {
        if(!root) return 0;
        int left=depth(root->left);
        int right=depth(root->right);
        return max(left,right)+1;
    }
```

