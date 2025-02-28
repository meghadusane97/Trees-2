# Trees-2

## Problem1 (https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)
```Java
class Solution {
    public TreeNode buildTree(int[] inorder, int[] postorder) {
        return build(0,inorder.length-1,0,postorder.length-1,inorder,postorder);
    }

    private TreeNode build(int istart,int iend,int pstart,int pend,int[]inorder, int[]postorder)
    {
        if(istart>iend || pstart>pend)
            return null;
        //find the index of root in the inoder subarray
        int rindex=findRootIndex(inorder,istart,iend,postorder[pend]);
        TreeNode root=new TreeNode(postorder[pend]);
        [Right-Array],root;
        int listart=istart;//listart indicates the index of left inoder-subarray start
        int liend=rindex-1;//liend indicates the index of left inoder-subarray end
        int lpstart=pstart; //lpstart indicates the index of left postoder-subarray start
        //since the number elements in the left-Array for both Inorder and Postorder sub-arrays are equal, hence we can write liend-listart=lpend-lpstart
        int lpend=liend-listart+lpstart;//lpend indicates the index of left postoder-subarray end
        //similarly these are for the right-subarray in inorder and postorder sub-arrays
        int ristart=rindex+1;
        int riend=iend;
        int rpstart=lpend+1;
        int rpend=pend-1;
        //calling left and right sub-arrays with the help of above indices
        root.left=build(listart,liend,lpstart,lpend,inorder,postorder);
        root.right=build(ristart,riend,rpstart,rpend,inorder,postorder);
        return root;
    }

    private int findRootIndex(int[]inorder,int start,int end,int val)
    {
        for(int i=start;i<=end;i++)
        {
            if(inorder[i]==val)
                return i;
        }
        return 0;
    }
}
```

## Problem2: sum-root-to-leaf-numbers

```Java
// Time Complexity : O(n)
// Space Complexity : O(n)
// Did this code successfully run on Leetcode : yes
// Any problem you faced while coding this : no

/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int sumNumbers(TreeNode root) {
        Stack<TreeNode> st = new Stack<>();
        Stack<Integer> numSt = new Stack<>();
        
        int sum = 0;
        int currNum = 0;
        
        while(root != null || !st.isEmpty()){
            while(root != null){
                currNum = currNum * 10 + root.val;
                st.push(root);
                numSt.push(currNum);
                root = root.left;
            }
            //pop
            root = st.pop();
            currNum = numSt.pop(); 
            
            //check leaf
            if(root.left == null && root.right == null)
                sum += currNum;
            
            root = root.right;
        }
        return sum;
    }
}
```
   
