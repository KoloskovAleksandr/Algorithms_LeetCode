# Trees

+ [Binary Tree Inorder Traversal](#binary-tree-inorder-traversal)
+ [Symmetric Tree](#symmetric-tree)
+ [Maximum Depth of Binary Tree](#maximum-depth-of-binary-tree)
+ [Same Tree](#same-tree)
+ [Invert Binary Tree](#invert-binary-tree)
+ [Path Sum](#path-sum)
+ [Subtree of Another Tree](#subtree-of-another-tree)
+ [Binary Tree Level Order Traversal](#binary-tree-level-order-traversal)
+ [Kth Smallest Element in a BST](#kth-smallest-element-in-a-bst)
+ [Validate Binary Search Tree](#validate-binary-search-tree)
+ [Binary Search Tree Iterator](#binary-search-tree-iterator)
+ [Inorder Successor in BST](#inorder-successor-in-bst)
+ [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
+ [Lowest Common Ancestor of a Binary Tree](#lowest-common-ancestor-of-a-binary-tree)

## Binary Tree Inorder Traversal

https://leetcode.com/problems/binary-tree-inorder-traversal/

```C++
class Solution {
public:
    vector<int> inorderTraversal(TreeNode* root) {
        vector<int> res;
        RecursivePass(root, res);
        return res;     
    }
    void RecursivePass(TreeNode* root, vector<int>& res){
        if(root){
            RecursivePass(root->left, res);
            res.push_back(root->val);
            RecursivePass(root->right, res);            
        }
    }
};
```

## Symmetric Tree

https://leetcode.com/problems/symmetric-tree/

```C++
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        return isMirror(root, root);        
    }
    bool isMirror(TreeNode* t1, TreeNode* t2) {
        if (!t1 && !t2) return true;
        if (!t1 || !t2) return false;
        return (t1->val == t2->val && isMirror(t1->right, t2->left) && isMirror(t1->left, t2->right));
    }
};
```

## Maximum Depth of Binary Tree

https://leetcode.com/problems/maximum-depth-of-binary-tree/

```C++
class Solution {
public:
    int maxDepth(TreeNode* root) {
        return root == NULL ? 0 : max(maxDepth(root -> left), maxDepth(root -> right)) + 1;        
    }
};
```

## Same Tree

https://leetcode.com/problems/same-tree/

```C++
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == NULL || q == NULL)  return (p == q);
        return (p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right, q->right));       
    }
};
```

## Invert Binary Tree

https://leetcode.com/problems/invert-binary-tree/

```C++
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (root){
           TreeNode* right = invertTree(root->right);
           TreeNode* left = invertTree(root->left);
           root->left = right;
           root->right = left;
        }
        return root;        
    }
};
```

## Path Sum

https://leetcode.com/problems/path-sum/

```C++
class Solution {
public:
    bool hasPathSum(TreeNode* root, int sum) {
        if (root == NULL) return false;
        if (root->val == sum && root->left ==  NULL && root->right == NULL) return true;
        return hasPathSum(root->left, sum - root->val) || hasPathSum(root->right, sum - root->val);        
    }
};
```

## Subtree of Another Tree

https://leetcode.com/problems/subtree-of-another-tree/submissions/

```C++
class Solution {
public:
    bool isSubtree(TreeNode* s, TreeNode* t){
        return s && (isSameTree(s, t) || isSubtree(s->left, t) || isSubtree(s->right, t));
    }
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if (p == NULL || q == NULL)  return (p == q);
        return (p->val == q->val && isSameTree(p->left, q->left) && isSameTree(p->right, q->right));       
    }
};
```

## Binary Tree Level Order Traversal

https://leetcode.com/problems/binary-tree-level-order-traversal/

```C++
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root){
	    vector<vector<int>> result;
        int level = 0;
    	RecursivePass(root, result, level);
    	return result;
    }
    void RecursivePass(TreeNode *root, vector<vector<int>> &result, int level){
    	if (!root) 	return;
        if (level == result.size())
    	    result.push_back(vector<int> {});
        result[level].push_back(root->val);
        RecursivePass(root->left, result, level + 1);
        RecursivePass(root->right, result, level + 1);
    }
};
```

## Kth Smallest Element in a BST

https://leetcode.com/problems/kth-smallest-element-in-a-bst/

```C++
class Solution {
public:
    int kthSmallest(TreeNode* root, int k) {
        vector<int> res;
        InorderTraversal(root, res);
        return res[k - 1];     
        
    }
    void InorderTraversal(TreeNode* root, vector<int>& res){
        if(root){
            InorderTraversal(root->left, res);
            res.push_back(root->val);
            InorderTraversal(root->right, res);            
        }
    }
};
```

## Validate Binary Search Tree

https://leetcode.com/problems/validate-binary-search-tree/

```C++
class Solution {
public:
    bool isValidBST(TreeNode* root) {
        return RecursivePass(root, NULL, NULL);        
    }
    bool RecursivePass(TreeNode* node, TreeNode* lower, TreeNode* upper) {
        if (!node) return true;
        int val = node->val;
        if ((lower && val <= lower->val) || (upper && val >= upper->val))
            return false;
        if (!RecursivePass(node->right, node, upper)) return false; 
        if (!RecursivePass(node->left, lower, node)) return false;
        return true;
  }
};
```

## Binary Search Tree Iterator

https://leetcode.com/problems/binary-search-tree-iterator/

```C++
class BSTIterator {
    stack<TreeNode*> Stack;
public:
    BSTIterator(TreeNode* root) {
        pushLeftEdge(root);        
    }
    int next() {
        TreeNode *tmp = Stack.top();
        Stack.pop();
        pushLeftEdge(tmp->right);
        return tmp->val;        
    }
    bool hasNext() {
        return !Stack.empty();        
    }
    void pushLeftEdge(TreeNode *node) {
        for (; node != NULL; Stack.push(node), node = node->left);
    }
};
```

## Inorder Successor in BST

https://www.lintcode.com/problem/inorder-successor-in-bst/

```C++
class Solution {
public:
    TreeNode* inorderSuccessor(TreeNode* root, TreeNode* p) {
        TreeNode* succ = NULL;
        if(root){
            if(p->right)
                for(succ = p->right; succ->left; succ = succ->left);
            else
                while (root->val != p->val)
                    root->val > p->val ? (succ = root, root = root->left) : root = root->right; 
            return succ;
        }
        return root;
    }
};
```

## Lowest Common Ancestor of a Binary Search Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-search-tree/

```C++
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        int pVal = p->val;
        int qVal = q->val;
        TreeNode* node = root;
        while(node) {
            int parentVal = node->val;
            if (pVal > parentVal && qVal > parentVal)
                node = node->right;
            else if (pVal < parentVal && qVal < parentVal)
                node = node->left;
            else return node;
        }
        return {};
    }
};
```

## Lowest Common Ancestor of a Binary Tree

https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/

```C++
class Solution {
public:
    TreeNode* ans = NULL;
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        scanTree(root, p, q);
        return ans;        
    }
    bool scanTree(TreeNode* currentNode, TreeNode* p, TreeNode* q) {
        if (!currentNode)   return false;

        int left = scanTree(currentNode->left, p, q);
        int right = scanTree(currentNode->right, p, q);
        int mid = (currentNode == p || currentNode == q);
        if (mid + left + right >= 2) 
            ans = currentNode;
        return (mid + left + right > 0);
    }
};
