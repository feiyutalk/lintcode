# Description

![](/images/construct_binary_tree.png)

***
## Aanalysis

根据前序和中序对应的数组来构造二叉树，记得这是考研的时候很喜欢出的题型，但是，当时的话，一般都是能够把二叉树画出来就可以了，没有涉及到代码实现。但是我们只要抓住了问题的本质，不管是画出图，还是代码实现，其解题的思路是没有什么变化的。都是先根据前序数组的第一根必定是根节点，然后根据中序数组根节点把左右子树进行划分的特点，来递归的求解本题。

## Solution
```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 */
 
 
public class Solution {
    /**
     *@param preorder : A list of integers that preorder traversal of a tree
     *@param inorder : A list of integers that inorder traversal of a tree
     *@return : Root of a tree
     */
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        // write your code here
        if(preorder.length == 0 )
            return null;
        if(preorder.length == 1 ){
            TreeNode root = new TreeNode(preorder[0]);
            return root;
        }
        
        int rootval = preorder[0];
        
        int index = 0;
        for(int i=0; i<inorder.length; i++){
            if(inorder[i] == rootval){
                index = i;
                break;
            }
        }
        
        int[] preleft = new int[index];
        int[] preright = new int[preorder.length - index - 1];
        for(int i = 1; i<=index; i++){
            preleft[i-1] = preorder[i];
        }
        for(int i = index+1; i<preorder.length; i++){
            preright[i-index-1] = preorder[i];
        }
        
        int[] inleft = new int[index];
        int[] inright = new int[preorder.length - index - 1];
        for(int i =0 ; i<index; i++){
            inleft[i] = inorder[i];
        }
        for(int i = index+1; i<inorder.length; i++){
            inright[i - index - 1] = inorder[i];
        }
        
        TreeNode root = new TreeNode(rootval);
        root.left = buildTree(preleft, inleft);
        root.right = buildTree(preright, inright);
        return root;
    }
}
```

***
enjoy life, coding now!:D