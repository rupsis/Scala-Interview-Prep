Problem:
```
Given the root of a binary tree, return the preorder traversal of its nodes' values.
```

```scala
Input: root = [1,null,2,3]
Output: [1,2,3]
```

<details><summary>Pre-order</summary>

```scala
/**
 * Definition for a binary tree node.
 * class TreeNode(_value: Int = 0, _left: TreeNode = null, _right: TreeNode = null) {
 *   var value: Int = _value
 *   var left: TreeNode = _left
 *   var right: TreeNode = _right
 * }
 */
object Solution {
    def preorderTraversal(root: TreeNode): List[Int] = {
        Option(root) match {
            case Some(node) => List(node.value) ++ preorderTraversal(node.left) ++ preorderTraversal(node.right)
            case _ => List()
        }
    }
}
```

Runtime: `O(N Log N)` 

</details>

<details><summary>In-order</summary>

```scala
def inorderTraversal(root: TreeNode): List[Int] = {
    Option(root) match {
        case Some(node) => inorderTraversal(node.left) ++ List(node.value) ++ inorderTraversal(node.right)
        case _ => List()
    }
}
```

Runtime: `O(N Log N)` 

</details>

<details><summary>Post-order</summary>

```scala
def postorderTraversal(root: TreeNode): List[Int] = {
        Option(root) match {
        case Some(node) => postorderTraversal(node.left) ++ postorderTraversal(node.right) ++ List(node.value)
        case _ => List()
    }
}
```

Runtime: `O(N Log N)` 

</details>

---