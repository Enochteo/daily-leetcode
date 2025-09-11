## Sorting Comparator
**Understand**

We are asked to sort a list of players by:

Score in descending order (higher scores come first).

If two players have the same score, sort them by name in ascending alphabetical order.

We are given a list of (name, score) pairs and must output them sorted according to these rules.

**Match**

This is a custom sorting problem:

Built-in sort normally uses numeric or lexicographic ordering.

Here we need a comparator function that compares two Player objects and enforces:

Higher score → comes earlier.

If scores equal → compare names alphabetically.

Python’s sorted() doesn’t take a comparator directly, but we can use functools.cmp_to_key to convert a comparator function into a key function.

**Plan**

Define a Player class with attributes name and score.

Implement a comparator(a, b) method:

If a.score > b.score: return -1 (a comes before b).

If a.score < b.score: return 1 (b comes before a).

Otherwise, compare a.name and b.name.

Use sorted(data, key=cmp_to_key(Player.comparator)) to sort the players.

Print the results.

**Implement**
```py
from functools import cmp_to_key

class Player:
    def __init__(self, name, score):
        self.name = name
        self.score = score
        
    def __repr__(self):
        return f'{self.name, self.score}'
        
    def comparator(a, b):
        if a.score != b.score:
            return -1 if a.score > b.score else 1
        else:
            return -1 if a.name < b.name else 1

n = int(input())
data = []
for i in range(n):
    name, score = input().split()
    score = int(score)
    player = Player(name, score)
    data.append(player)
    
data = sorted(data, key=cmp_to_key(Player.comparator))
for i in data:
    print(i.name, i.score)
```

**Review**

Custom comparator enforces descending score, then ascending name order.

cmp_to_key adapts the comparator for Python’s sort.

Prints sorted players in the correct order.

**Evaluate**

Time Complexity: Sorting → O(n log n)

Space Complexity: O(n) for storing players.

Efficient for HackerRank constraints.