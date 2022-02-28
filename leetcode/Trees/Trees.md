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

</details>

<details><summary>Breadth First Search (BFS)</summary>

```scala
import scala.collection.mutable.ListBuffer
object Solution {
    def levelOrder(root: TreeNode): List[List[Int]] = {

      var levels = mutable.ListBuffer[ListBuffer[Int]]()

      def nextLevel(node: TreeNode, level: Int): Unit = {

        if(levels.length == level) levels += ListBuffer()

        levels(level) += node.value

        if(node.left != null) nextLevel(node.left, level + 1)
        if(node.right != null) nextLevel(node.right, level + 1)

      }

      Option(root) match {
          case Some(node) => nextLevel(node, 0)
          case None => levels
      }

      levels.map(_.toList).toList
    }
}
```

Runtime: `O(N)` 

</details>

---

</details>

<details><summary>Max Depth</summary>

This one is kinda a gimmy. We can easily compute the max depth by using a BFS
and then getting the size of the list (which is the max depth)

```scala
object Solution {
    import collection.mutable._
    def maxDepth(root: TreeNode): Int = {

      var levels = ListBuffer[ListBuffer[Int]]()

      def nextLevel(node: TreeNode, level: Int): Unit = {

        if(levels.length == level) levels += ListBuffer()

        levels(level) += node.value

        if(node.left != null) nextLevel(node.left, level + 1)
        if(node.right != null) nextLevel(node.right, level + 1)
      }

      Option(root) match {
          case Some(node) => nextLevel(node, 0)
          case None => levels
      }

      levels.length
    }
}
```

Runtime: `O(N)` 

</details>

---

<details><summary>isSymmetric</summary>

Got kinda lazy on this one. Reused inorderTraversal with a little logic at the bottom. 

```scala
object Solution {
  def isSymmetric(root: TreeNode): Boolean = {
    def inorderTraversal(root: TreeNode, side: Char): List[(Int, Char)] = {
      Option(root) match {
        case Some(node) => inorderTraversal(node.left, 'l') ++ List((node.value, side)) ++ inorderTraversal(node.right, 'r')
        case _ => List()
      }
    }
    
    val left = inorderTraversal(root.left, 'l')
    val right = inorderTraversal(root.right, 'r')

    left.zip(right.reverse).forall { item =>
      item._1._1 == item._2._1 && item._1._2 != item._2._2
    } && left.size == right.size

  }
}
```

Runtime: `O(N)` 

</details>

---

