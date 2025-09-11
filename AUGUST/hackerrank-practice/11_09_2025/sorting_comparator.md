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