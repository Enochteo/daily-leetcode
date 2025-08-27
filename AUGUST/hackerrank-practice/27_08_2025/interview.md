## The Full Counting Sort -> 
*https://www.hackerrank.com/challenges/countingsort4/problem?isFullScreen=true*
**Solution**:
```py
def countSort(arr):
   counts = [[] for _ in range(n)]
   counter = 0
   for num, string in arr:
       if counter == n/2:
           break
       counter += 1
       counts[int(num)].append('-')
   for index in range(counter, n):
       counts[int(arr[index][0])].append(arr[index][1])
   res = ''
   for line in counts:
       res += ' '.join(line)
       res += ' '
   print(res.strip())
```