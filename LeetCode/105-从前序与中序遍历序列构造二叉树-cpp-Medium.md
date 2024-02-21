# 105 从前序与中序遍历序列构造二叉树

给定两个整数数组 `preorder` 和 `inorder` ，其中 `preorder` 是二叉树的先序遍历， `inorder` 是同一棵树的中序遍历，请构造二叉树并返回其根节点。

示例 1:

    输入: preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
    输出: [3,9,20,null,null,15,7]

示例 2:

    输入: preorder = [-1], inorder = [-1]
    输出: [-1]

提示:

- `1 <= preorder.length <= 3000`
- `inorder.length == preorder.length`
- `-3000 <= preorder[i], inorder[i] <= 3000`
- `preorder` 和 `inorder` 均 无重复 元素
- `inorder` 均出现在 `preorder`
- `preorder` **保证** 为二叉树的前序遍历序列
- `inorder` **保证** 为二叉树的中序遍历序列

```cpp
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
    TreeNode* makeTree(vector<int>& preorder, vector<int>inorder, int pre_l, int pre_r, int in_l, int in_r) {
        if(in_l == in_r)
            return nullptr;
        int i = 0;
        for(i = 0; i < in_r; i++) {
            if(inorder[i] == preorder[pre_l])
                break;
        }
        int left_num = i - in_l;
        int right_num = in_r - i - 1;
        TreeNode* left_node = makeTree(preorder, inorder, pre_l+1, pre_l+1+left_num, in_l, i);
        TreeNode* right_node = makeTree(preorder, inorder, pre_r-right_num, pre_r, i+1, in_r);
        auto tmp = new TreeNode(inorder[i], left_node, right_node);
        return tmp;
    }
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return makeTree(preorder, inorder, 0, preorder.size(), 0, inorder.size());
    }
};
```
