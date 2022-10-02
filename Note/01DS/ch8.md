## 前、中、后、层序遍历

**[144. 二叉树的前序遍历](https://leetcode.cn/problems/binary-tree-preorder-traversal/)**

**函数递归**

```cpp
class Solution {
public:
    vector<int> ans;
    void traversal(TreeNode* node){
        ans.push_back(node->val);
        if(node->left) traversal(node->left);
        if(node->right) traversal(node->right);
    }
    vector<int> preorderTraversal(TreeNode* root) {
        if(root) traversal(root);
        return ans;
    }
};
```

**统一迭代法**

```cpp
class Solution {
public:
    vector<int> preorderTraversal(TreeNode* root) {
        vector<int> ans;
        stack<TreeNode*> st;
        if(root) st.push(root);
        while(!st.empty()){
            TreeNode* node = st.top();
            st.pop();
            if(node){
                if(node->right) st.push(node->right);
                if(node->left) st.push(node->left);
                st.push(node);
                st.push(NULL);
            }
            else{
                node = st.top();
                st.pop();
                ans.push_back(node->val);
            }
        }
        return ans;
    }
};
```

**[94. 二叉树的中序遍历](https://leetcode.cn/problems/binary-tree-inorder-traversal/)**

**函数递归**

```cpp
class Solution {
public:
    void traversal(TreeNode* node, vector<int>& ans){
        if(node->left) traversal(node->left, ans);
        ans.push_back(node->val);
        if(node->right) traversal(node->right, ans);
        return;
    }
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> ans;
        if(root) traversal(root, ans);
        return ans;
    }
};
```

**统一迭代法**

```cpp
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        stack<TreeNode*> st;
        vector<int> ans;
        if(root) st.push(root);
        while(!st.empty()){
            TreeNode* node = st.top();
            st.pop();
            if(node){
                if(node->right) st.push(node->right);
                st.push(node);
                st.push(NULL);
                if(node->left)  st.push(node->left);;
            }
            else{
                node = st.top();
                st.pop();
                ans.push_back(node->val);
            }
        }
        return ans;
    }
};
```

**[145. 二叉树的后序遍历](https://leetcode.cn/problems/binary-tree-postorder-traversal/)**

**函数递归**

```cpp
class Solution {
public:
    void traversal(TreeNode* node, vector<int>& ans){
        if(node->left) traversal(node->left, ans);
        if(node->right) traversal(node->right, ans);
        ans.push_back(node->val);
        return;
    }
    vector<int> postorderTraversal(TreeNode* root) {
        vector<int>ans;
        if(root) traversal(root, ans);
        return ans;
    }
};
```

**统一迭代法**

```cpp
class Solution {
public:
    vector<int> postorderTraversal(TreeNode* root) {
        stack<TreeNode*> st;
        vector<int> ans;
        if(root) st.push(root);
        while(!st.empty()){
            TreeNode* node = st.top();
            st.pop();
            if(node){
                st.push(node);
                st.push(NULL);
                if(node->right) st.push(node->right);
                if(node->left)  st.push(node->left);;
            }
            else{
                node = st.top();
                st.pop();
                ans.push_back(node->val);
            }
        }
        return ans;
    }
};
```

**[102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)**

```cpp
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        queue<TreeNode*>st;
        vector<vector<int>> ans;
        if(root) st.push(root);

        while(!st.empty()){
            int size = st.size();
            vector<int>vec;
            for(int i = 0; i < size; i++){
                TreeNode* node = st.front();
                st.pop();
                vec.push_back(node->val);
                if(node->left) st.push(node->left);
                if(node->right) st.push(node->right);
            }
            ans.push_back(vec);
        }
        return ans;
    }
};
```

---

## 例题

**[226. 翻转二叉树](https://leetcode.cn/problems/invert-binary-tree/)**

> 模板题。

**[101. 对称二叉树](https://leetcode.cn/problems/symmetric-tree/)**

> 二刷错误。没有正确处理空节点情况。
>
> 对于基础语法错误，还是要仔细看清楚。
>
> 一刷时候取巧用了特殊值标记。

**[104. 二叉树的最大深度](https://leetcode.cn/problems/maximum-depth-of-binary-tree/)**

> 一刷二刷的层次遍历是比较熟悉。
>
> 用前序遍历时，注意空节点处理。

**[111. 二叉树的最小深度](https://leetcode.cn/problems/minimum-depth-of-binary-tree/)**

> 这题一开始我就按照上面的思路写了一遍，但是忽略了本地中的定义，最小深度是从根节点到最小的叶子节点的最短路径上的节点数量。
>
> 所以当某个节点的左节点为空时不代表子树的高度就是1，应该分三类讨论：左节点为空，右节点不为空时为1+ lenr，同理 1 + lenl，如果都不为空时才是 1 + min( lenr, lenl)

**[222. 完全二叉树的节点个数](https://leetcode.cn/problems/count-complete-tree-nodes/)**

> 模板题。

**[110. 平衡二叉树](https://leetcode.cn/problems/balanced-binary-tree/)**

> 第一遍，遍历每个节点，判断每一棵子树是否是平衡二叉树。

**[257. 二叉树的所有路径](https://leetcode.cn/problems/binary-tree-paths/)**

> 初看的时候想到这是二叉树的前序遍历，遍历叶子节点的路径。
>
> 我怎么回退不同的路径呢？其实这题也可以说是回溯题，可以增加path存放遍历答案，再加上终止的条件。
>
> 回溯的几个要素：递归函数的参数，递归的终止条件，单层递归的逻辑。

**[404. 左叶子之和](https://leetcode.cn/problems/sum-of-left-leaves/)**

> 简单的遍历题，判断是不是左叶子节点即可。

**[112. 路径总和](https://leetcode.cn/problems/path-sum/)**

> 树的回溯题。
>
> 注意题目的值范围，可能包含负值的，所以在没有到叶子节点前，不能用sum> targetsum 剪枝。

**[106. 从中序与后序遍历序列构造二叉树](https://leetcode.cn/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)**

> 中等题。
>
> 思路我们可以从后序遍历末尾找到根节点，再从中序遍历中找到根节点的左子树序列和右子树序列。
>
> 后序遍历除去根节点以后，剩余的部分，我们可以根据上面已经划分好的左子树序列长度和右子树序列长度，然后将后序遍历的数组划分为左子树和右子树。然后继续划分左子树部分和右子树部分，当作根节点。
>
> 递归函数参数：中序数组、后序数组
>
> 终止条件：空节点，叶子节点
>
> 单循环：划分中序，划分后序，再子树划分

