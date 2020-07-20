https://blog.csdn.net/Sengo_GWU/article/details/81879502  
## Level by level
662. Maximum Width of Binary Tree
103. Binary Tree Zigzag Level Order Traversal
102. Binary Tree Level Order Traversal
958. Check Completeness of a Binary Tree  

## Index nodes
655. Print Binary Tree  
314. Binary Tree Vertical Order Traversal   

## Inorder
783. Minimum Distance Between BST Nodes  
285. Inorder Successor in BST      
99. Recover Binary Search Tree  
94. Binary Tree Inorder Traversal  
230. Kth Smallest Element in the BST

## DFS Deep/Height
979. Distribute Coins in Binary Tree  
```python
class Solution(object):
    res = 0
    def distributeCoins(self, root):
        def dfs(node):
            if not node: return 0
            left = dfs(node.left)
            right = dfs(node.right)
            self.res += abs(left) + abs(right)  # 这里有绝对值
            return node.val + left + right - 1  # node val
        dfs(root)
        return self.res
```

333. Largest BST Subtree   

222. Count Complete Tree Nodes

543. Diameter of Binary Tree  
124. Binary Tree Maximun Path Sum
865. Smallest Subtree with all the Deepest Nodes  
366. Find Leaves of Binary Tree  

## Serialize / Construct Tree
297. Serialize and Deserialize Binary Tree
449. Serialize and Deserialize BST
106. Construct Binary Tree from Inorder and Postorder Traversal   
105. Construct Binary Tree from Preorder and Inorder Traversal  
536. Construct Binary Tree from String  


## Others 
450. Delete Node in a BST  
437. Path Sum III   
617. Merge Two Binary Trees   
652. Find Duplicate Subtrees  
426. Convert Binary Search Tree to Sorted Doubly Linked List  
572. Subtree of Another Tree  
236. Lowest Common Ancestor of a Binary Tree  
```java
public class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if(root == null || root == p || root == q)  return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p, q);
        if(left != null && right != null)   return root;
        return left != null ? left : right;
    }
}
```
235. Lowest Common Ancestor of a Binary Search Tree   
545. Boundary of Binary Tree  
