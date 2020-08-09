## 学习笔记

> HashMap总结



> 有效的字母异位词



> 字母异位词分组



> 两数之和



------

> 树基础知识



树与图之间的差别在于有没有环，图可以有环。可以将链表理解为特殊的树，树理解为特殊的图。

**树节点的定义：**

```java
class TreeNode{

	public int val;
	public TreeNode left,right;
	
}
```

**树的遍历**

1. 前序：根-左-右
2. 中序：左-根-右
3. 后序：左-右-根



> 二叉搜索树

二叉搜索树又称为二叉排序树

1. 左子树上所有的节点都小于它的根节点
2. 右子树上的节点的值均大于根节点值结论

**结论**：中序遍历是一个升序排序



**二叉树常见操作：**

1. 查询  O(logn)
2. 插入 O(logn)
3. 删除：O(logn)  删除叶子的话直接删除   删除的子树的根节点的话需要找右子树第一个大于被删的节点的节点来替换



特殊的二叉搜索树： 比如 1 2 3 4 5 6 7 8 9   这样的树只有右子树，相当于退化成链表，查询插入删除时间复杂度也退化成了O(n),所以为了解决这个问题出现了**平衡二叉树**



> 二叉树中序遍历

时间复杂度：O（n）

空间复杂度：最坏O(n)  平均O(logn)  

```java
public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> datas = new ArrayList<>();
        helper(datas, root);
        return datas;
    }

    private void helper(List<Integer> datas, TreeNode root) {

        if (root != null) {
            //TODO  左子树
            helper(datas, root.left);
            //TODO 根节点
            datas.add(root.val);
            //TODO  右子树
            helper(datas, root.right);

        }
    }
```

> 二叉树前序遍历

```java
 public List<Integer> preorderTraversal(TreeNode root) {

         List<Integer> datas = new ArrayList<>();

         helper(datas,root);

         return datas;   

    }
      private void  helper( List<Integer> datas,TreeNode root){

        if(root!=null){
            //TODO 根节点
            datas.add(root.val);
            //TODO 左子树
            helper( datas, root.left);
            //TODO 右子树
             helper( datas, root.right);
        }

      }
```



> 实战

- [二叉树的中序遍历](https://leetcode-cn.com/problems/binary-tree-inorder-traversal/)（亚马逊、微软、字节跳动在半年内面试中考过）
- [二叉树的前序遍历](https://leetcode-cn.com/problems/binary-tree-preorder-traversal/)（谷歌、微软、字节跳动在半年内面试中考过）
- [N 叉树的后序遍历](https://leetcode-cn.com/problems/n-ary-tree-postorder-traversal/)（亚马逊在半年内面试中考过）
- [N 叉树的前序遍历](https://leetcode-cn.com/problems/n-ary-tree-preorder-traversal/description/)（亚马逊在半年内面试中考过）
- [N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)



> 二叉堆

通过完全二叉树实现，注意不是二叉搜索树，根和每一级节点都是满的除了最下面一级叶子可能不满之外

**二叉堆（大堆）性质**：

1. 是一棵完全树
2. 树中任意节点的值总是>=其子节点的值

**二叉堆实现**

1. 一般通过数组实现

2. 假设第一个元素在数组中的索引为0的话，则父节点和子节点的位置关系如下：

   索引为i的左孩子的索引是2*i+1

   索引为i的右孩子的索引是2*i+2

   索引为i的父节点的索引是floor((i-1)/2)

**插入数据 **



> 做题四件套

1. 和面试官把题目过一遍

2. 在所有解中找出最优的解

3. coding

4. test cases

   

