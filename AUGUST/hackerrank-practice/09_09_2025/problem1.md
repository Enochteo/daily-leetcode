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