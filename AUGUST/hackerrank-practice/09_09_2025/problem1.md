## Roads and Libraries
**Problem Statement**

The government of a country wants to ensure that every citizen has access to a library. The country has n cities and m possible bidirectional roads. Building infrastructure has costs:

`c_lib`: Cost of building a library in a city.

`c_road`: Cost of building a road between two cities.

Every citizen must be able to access a library, either:

By having one in their city, or

By traveling along roads to reach a city with a library.

Your task is to determine the minimum cost to provide library access to all citizens.

**Input Format**

The first line contains an integer q, the number of queries.

For each query:

First line: n m c_lib c_road

Next m lines: two integers u v, denoting a road between city u and city v.

**Output Format**

For each query, print a single integer: the minimum cost.

**Constraints**

1 ≤ q ≤ 10

1 ≤ n ≤ 10^5

0 ≤ m ≤ 10^5

1 ≤ c_lib, c_road ≤ 10^5

1 ≤ u, v ≤ n


**Approaches**
1. Graph Traversal (DFS/BFS)

Build adjacency list for the cities.

Traverse unvisited nodes, count component size.

Apply formula for each component.

2. Union-Find (Disjoint Set Union - DSU)

Initialize n disjoint sets.

For each road (u, v), perform union(u, v).

After all unions, count size of each disjoint set.

Apply formula for each set.

**Pseudocode (DFS)**
```py
def roadsAndLibraries(n, c_lib, c_road, roads):
    if c_lib <= c_road:
        return n * c_lib
    
    graph = build adjacency list from roads
    visited = [False] * (n+1)
    total_cost = 0
    
    for city in range(1, n+1):
        if not visited[city]:
            size = dfs_count(city)
            total_cost += c_lib + (size - 1) * c_road
    
    return total_cost
```