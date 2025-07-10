## Permutations
**Understand**
Given a list of distinct integers, return all possible permutations of the numbers.

**Match**
Problem Type: Backtracking / Recursion

Data Structure: List of permutations

Algorithm: Recursive insert-and-build pattern

**Plan**
Base case: the permutation of an empty list is [[]].

Recursive step:

Remove the first element.

Recursively find all permutations of the rest.

Insert the first element at every possible position in each of the smaller permutations.

**Implement**
Recursively call permute on nums[1:].

Loop through each returned permutation and insert nums[0] at every index.

Build and collect all resulting permutations.

**Review**
Uses recursion and insertions to generate all permutations.

p_copy.insert(i, nums[0]) handles positional variations.

Handles base case of empty list.

**Evaluate**
Time Complexity: O(n!) – there are n! permutations for n elements.

Space Complexity: O(n!) for storing all permutations

**Pattern to remeber by:** Recursive insertion to generate all permutations of input array