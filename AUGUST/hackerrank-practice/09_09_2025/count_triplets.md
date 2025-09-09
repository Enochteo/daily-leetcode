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