## 2D Array Problem
***https://www.hackerrank.com/challenges/2d-array/problem
```py
def hourglassSum(arr)***:
   # Write your code here
   max_sum = float('-inf')
   def calculate_hour_glass_sum(i, j):
       total = 0
       hour_glass = [(0,0), (0,1), (0,2), (1,1), (2,0), (2,1), (2,2)]
       for di, dj in hour_glass:
           total += arr[i + di][j + dj]
       return total
   for r in range(4):
       for c in range(4):
           max_sum = max(max_sum, calculate_hour_glass_sum(r, c))
   return max_sum
```
*** Pattern used ***: Matrix traversal, max sum
 **Time complexity**: O(16) -> O(1), space: O(1)
 **Bug**: used a wrong max_sum so the comparison was not made well 

## Left Rotation
***https://www.hackerrank.com/challenges/array-left-rotation/problem***
```py
def rotateLeft(d, arr):
   # Write your code here
   def reverse(nums, i, j):
       while i< j:
           nums[i], nums[j] = nums[j], nums[i]
           i += 1
           j -= 1
   reverse(arr, 0, (d%n)-1)
   reverse(arr, d%n, n-1)
   reverse(arr, 0, n-1)
   return arr
```