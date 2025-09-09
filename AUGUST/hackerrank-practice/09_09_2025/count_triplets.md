## Count Triplets
**Problem**

We want to count triplets (i, j, k) such that:

i < j < k

arr[j] = arr[i] * r

arr[k] = arr[j] * r

**Understand**

We are asked to generate all structurally unique BSTs (binary search trees) that store values 1..n.

Each BST must follow the BST property:

Left subtree values < root < Right subtree values.

Different structures count as different BSTs, even if they contain the same values.

We must return all possible root nodes representing distinct BSTs.

**Match**

This is a recursive tree construction problem:

Pick each number val in `[left..right]` as the root.

Recursively generate all possible left subtrees from `[left..val-1]`.

Recursively generate all possible right subtrees from `[val+1..right]`.

Combine every left and right subtree with the chosen root.

Base cases:

If left > right: return `[None]` (empty tree).

If left == right: return `[TreeNode(left)]`.