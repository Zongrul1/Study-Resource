# 题目描述
给定一棵二叉搜索树，请找出其中的第k小的结点。例如， （5，3，7，2，4，6，8）    中，按结点数值大小顺序第三小结点的值为4。

# 解法
中序递归：

```java
/*
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
import java.util.*;
public class Solution {
    private ArrayList<TreeNode> result;
    private int depth;
    TreeNode KthNode(TreeNode pRoot, int k)
    {
        if(k < 1){
            return null;
        }
        depth = 0;
        result = new ArrayList<TreeNode>();
        Traverse(pRoot);
        if(k > depth){
            return null;
        }
        return result.get(k - 1);
    }
    void Traverse(TreeNode node){
        if(node != null){
            depth++;
            Traverse(node.left);
            result.add(node);
            Traverse(node.right);
        }
    }

}
```

中序非递归：

```java
import java.util.*;
public class Solution {
    TreeNode KthNode(TreeNode root, int k) {
        if(root == null || k == 0) return null;
        int count = 0;
        Stack<TreeNode> stack = new Stack<>();
        while (root != null || ! stack.isEmpty()) {
            while (root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            count ++;
            if(count == k) return root;
            root = root.right;
        }
        return null;
    }
}
```
