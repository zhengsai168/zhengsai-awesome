```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def minCameraCover(self, root: TreeNode) -> int:
        if root.left == None and root.right==None:
            return 1
        def dfs(x):
            if x==None:
                return 0,0,0
            if x.left == None and x.right == None:
                return 0,1,0
            s1,f1,t1 = dfs(x.left)
            s2,f2,t2 = dfs(x.right)
            s,f,t = 0,0,0
            if t1==0 and t2==0:
                f = 1
            if f1 or f2:
                t = 1
                f = 0
            return s1+s2+t,f,t
        ans,_1,_2 = dfs(root)
        return ans+_1
```

