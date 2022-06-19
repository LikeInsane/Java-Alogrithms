# 树与图，二叉堆，二叉搜索树
## 第一题：从中序与后序遍历序列构造二叉树 https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/
```java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        this.inorder = inorder;
        this.postorder = postorder;
        return build(0, postorder.length-1, 0, inorder.length-1);

    }

    TreeNode build(int l1, int r1, int l2, int r2){
        if(l1 > r1) return null;
        TreeNode root = new TreeNode(postorder[r1]);
        int mid = l2;
        while(inorder[mid]!=root.val) mid++;
        //左子树中序：l2~mid-1
        //右子树中序：mid+1~r2
        root.right=build(l1+(mid-l2), r1-1, mid+1, r2);
        root.left=build(l1, l1+(mid-l2)-1, l2, mid-1);
        return root;
    }

    int[] inorder;
    int[] postorder;
}
```

## 第二题：把二叉搜索树转换为累加树 https://leetcode.cn/problems/convert-bst-to-greater-tree/
```java
class Solution {
    private int sum=0;
    public TreeNode convertBST(TreeNode root) {
        /**
         * 题目求等于且大于当前值的节点和，并以此更新当前节点值
         * 因为bts中序遍历可得到单调递增数组，因此反向中序遍历即可拿到递减数组
         * 以此累加求和即可
         * */
        
        if(root != null){
            convertBST(root.right);
            sum+=root.val;
            root.val=sum;
            convertBST(root.left);
        }
        return root;
    }
}
```

## TODO: 将后续题刷完
