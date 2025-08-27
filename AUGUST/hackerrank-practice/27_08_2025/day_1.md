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

## Bear and Steady Gene -> 
*https://www.hackerrank.com/challenges/bear-and-steady-gene/problem*
**Solution**:
```py
from collections import Counter

def steadyGene(gene: str) -> int:
    n = len(gene)
    target = n // 4
    cnt = Counter(gene)

    need = {ch: max(0, cnt[ch] - target) for ch in 'ACGT'}
    if all(v == 0 for v in need.values()):
        return 0

    def covers(have):
        # return True if have[ch] >= need[ch] for all ch
        return all(have[ch] >= need[ch] for ch in need)

    ans = n
    have = Counter()
    l = 0
    for r, ch in enumerate(gene):
        if need[ch] > 0:        # only track letters that matter
            have[ch] += 1

        while l <= r and covers(have):
            ans = min(ans, r - l + 1)
            left_ch = gene[l]
            if need[left_ch] > 0:
                have[left_ch] -= 1
            l += 1

    return ans
```

## Lily’s Homework
**Solution**:
```py
def lilysHomework(arr):
    def count_swaps(a, target):
        a = a[:]                              # work on a copy
        pos = {v: i for i, v in enumerate(a)} # value -> current index
        swaps = 0
        for i in range(len(a)):
            correct = target[i]
            if a[i] != correct:
                j = pos[correct]              # where the correct value currently is
                # swap a[i] <-> a[j]
                pos[a[i]] = j
                pos[correct] = i
                a[i], a[j] = a[j], a[i]
                swaps += 1
        return swaps

    asc = sorted(arr)
    dsc = asc[::-1]
    return min(count_swaps(arr, asc), count_swaps(arr, dsc))
```