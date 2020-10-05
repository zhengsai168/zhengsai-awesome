# 链表

- 遍历

#### [2. Add Two Numbers](https://leetcode-cn.com/problems/add-two-numbers/)

# 二叉树

- 层次遍历

[117. 填充每个节点的下一个右侧节点指针 II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)

- 前/中/后序遍历

```python
class TreeNode:
    def __init__(self, val=0, left=None, right=None):
        self.val = val
        self.left = left
        self.right = right
前序：
访问root
dfs(root.left)
dfs(root.right)
中序：
dfs(root.left)
访问root
dfs(root.right)
后序：
dfs(root.left)
dfs(root.right)
访问root
```

#### [145. 二叉树的后序遍历](https://leetcode-cn.com/problems/binary-tree-postorder-traversal/)

# BST(Binary Search Tree，二叉搜索树/查找/排序树)

- 插入操作

#### [701. 二叉搜索树中的插入操作](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)

# 枚举

- 二进制枚举

#### [1601. 最多可达成的换楼请求数目](https://leetcode-cn.com/problems/maximum-number-of-achievable-transfer-requests/)

# DP
#### [LCP 19. 秋叶收藏集](https://leetcode-cn.com/problems/UlBDOe/)
- 描述： 将一个只有r和y的字符串（例如"rrryyyrryyyrr"），转换为转换为 ryr 这样的字符串序列，至少需要替换几次？
- dp方程： dp[i][0],dp[i][1],dp[i][2] 代表到第i个字符串，状态为0（r），1（ry），2（ryr）需要几次？

# 双指针

#### [18. 4Sum](https://leetcode-cn.com/problems/4sum/)

- n2枚举前两个数，双指针搞定后两个数，注意去重。

