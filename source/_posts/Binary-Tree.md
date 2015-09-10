title: Binary Tree
date: 2015-08-04 15:28:14
tags: Binary Tree
categories: Data Structure

---

{% blockquote %}
A binary tree is a tree data structure in which each node has at most two children, which are referred to as the left child and the right child.
{% endblockquote %}

Typically binary tree is used to define a labeling function on the nodes, which associates some value to each node. Binary trees labelled this way are used to implement `binary search trees` and `binary heaps`, and are used for efficient searching and sorting.
<!--more-->
## Binary Search Tree
{% blockquote %}
A binary search tree is a rooted binary tree, whose internal nodes each stores a key (and optionally, an associated value) and each has two distinguished sub-trees, commonly denoted left and right. The tree additionally satisfies the binary search tree property, which states that the key in each node must begreater than all keys stored in the left sub-tree and smaller than all keys in right sub-tree.
{% endblockquote %}
When looking for a key in a BST, we traverse the tree from root to leaf, making comparisons to keys stored in the nodes of the tree and deciding, based on the comparison, to continue searching in the left or right subtrees. On average, this means that each comparison allows the operations to skip about half of the tree, so that each lookup, insertion or deletion takes time proportional to the logarithm of the number of items stored in the tree.

## Binary Heap

A binary heap is a heap data structure created using a binary tree. It can be seen as a binary tree with two additional constrains:
### Shape property
{% blockquote %}
A binary heap is a complete binary tree; that is, all leaves of the tree, except possibly the last one (deepest) are full filled, and if the last level of the tree is not complete, the nodes of that level are filled from left to right.
{% endblockquote %}
### Heap property
{% blockquote %}
All nodes are either greater than or equal to or less than or equal to each of its children, according to a comparison predicate defined for the heap.
{% endblockquote %}
Heaps with a mathematical "greater than or equal to" (>=) comparison predicate are called max-heaps; those with a mathematical "less than or equal to" (<=) comparison predicate are called min-heaps. Min-heaps are often used to implement priority queues.
<u>
    Tip: B-tree is a tree data structure that keeps data sorted and allows searches, sequential access, insertions, and deletions in logarithmic time. The B-tree is a generalization of a binary search tree in that a node can have more than two children. It's usually used in index of database.
</u>

## Balanced Binary Tree
{% blockquote %}
Given a binary tree, determine if it is height-balanced.
For this problem, a height-balanced binary tree is defined as a binary tree in which the depth of the two subtrees of every node never differ by more than 1.
{% endblockquote %}

``` bash
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    bool isBalanced(TreeNode* root) {
        if(root == NULL) {
            return true;
        }
        int diff = maxDepth(root -> left) - maxDepth(root -> right);
        if(diff > 1 || diff < -1) {
            return false;
        }
        return isBalanced(root -> left) && isBalanced(root -> right);
    }
    
    int maxDepth(TreeNode* root) {
        if(root == NULL){
            return 0;
        }
        int lMaxDepth = maxDepth(root -> left);
        int rMaxDepth = maxDepth(root -> right);
        return 1 + (lMaxDepth > rMaxDepth ? lMaxDepth : rMaxDepth);
        // here will get a Time Limit Exceeded directly use:
        // return 1 + ((maxDepth(root -> left) > maxDepth(root -> right)) ? maxDepth(root -> left) : maxDepth(root -> right));
    }
};
```
