## Crossword Puzzle
**Understand**

We are asked to fill a 10x10 crossword grid with a given set of words.

The crossword is represented by a list of strings, where:

'-' represents an empty cell where letters can be placed.

'+' represents a blocked cell.

We are given words in the form "WORD1;WORD2;WORD3;...".

Each word must be placed horizontally or vertically.

The filled crossword must be valid — all words must fit exactly, align properly, and not conflict with other words.

This is a constraint satisfaction problem, well-suited to backtracking recursion.