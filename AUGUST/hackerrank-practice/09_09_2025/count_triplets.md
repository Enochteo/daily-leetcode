## Count Triplets
**Problem**

We want to count triplets (i, j, k) such that:

i < j < k

arr[j] = arr[i] * r

arr[k] = arr[j] * r

**Understand**

We are asked to count the number of triplets (i, j, k) in an array arr such that:

`i < j < k`

`arr[j] = arr[i] * r`

`arr[k] = arr[j] * r`

Where r is the given common ratio.

The array can be large (n ≤ 10^7 in constraints), so brute force checking all triplets is infeasible.

**Match**

This is a geometric progression detection problem:

Each element can potentially be:

the first element of a triplet,

the middle element of a triplet,

or the last element of a triplet.

Key observation:
When we process num as the middle element, the number of valid triplets is:

count += (# of left elements equal to num/r) * (# of right elements equal to num*r)


We need efficient frequency lookups on both sides.

**Plan**

Use two hash maps (dictionaries):

left_map: counts of numbers we’ve already passed (potential left side).

right_map: counts of numbers still ahead (potential right side).

Initialize right_map as a frequency count of all numbers in arr.

For each number num in arr:

Decrement right_map[num] since we’re processing it now.

If num % r == 0:

Add left_map[num // r] * right_map[num * r] to result.

Increment left_map[num] since num now becomes part of the left side.

Return the total count.

**Implement**
```py
from collections import defaultdict, Counter

def countTriplets(arr, r):
    counts = 0
    left_map = defaultdict(int)
    right_map = Counter(arr)  # counts of all elements to the right initially
    
    for num in arr:
        right_map[num] -= 1  # move current num from right to middle
        
        if num % r == 0:  # num can only be a middle if divisible by r
            counts += left_map[num // r] * right_map[num * r]
        
        left_map[num] += 1  # move current num to the left
    
    return counts
```

**Review**

Each element is treated as the middle of a potential triplet.

Efficient dictionary lookups allow O(1) checking of left/right candidates.

Avoids O(n³) or O(n²) brute force — runs in O(n).

**Evaluate**

Time Complexity:

O(n), since we make one pass through the array and use hash lookups.

Space Complexity:

O(n) for the hash maps in the worst case (all numbers unique).

**Pattern to Remember**

For problems involving triplets in geometric progression:

Use hash maps to track frequency of left and right candidates.

Treat each element as the potential middle of a triplet.

Count combinations dynamically without explicitly building all triplets.

This “left–middle–right” frequency product pattern is useful in:

Count Triplets (HackerRank)

Subsequence problems with ratios or differences

Triplet problems reducible to pair counting on both sides gyffuh