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

**Match**

This problem matches the backtracking / DFS search pattern:

Pick a word to place.

Try to place it in every valid horizontal or vertical position.

If a placement is valid, recursively attempt to place the next word.

If all words are placed, return the solution.

If not, undo the placement (backtrack) and try another option.

**Plan**

Preprocess input:

Split the words string by ;.

Convert the crossword grid into a mutable 2D list.

Helper functions:

can_place_h(r, c, word): Check if a word fits horizontally at (r, c).

can_place_v(r, c, word): Check if a word fits vertically at (r, c).

place_horizontal(r, c, word) / place_vertical(r, c, word): Place word, record changed positions.

unplace(placed): Undo a placement by restoring '-' in changed cells.

Backtracking recursion:

Base case: if all words are placed, return True.

Recursive step: try each word in each valid position.

If a placement leads to a solution, return True. Otherwise backtrack.

Return solution: Join the grid back into a list of strings.

**Implement**
```py
from collections import defaultdict, Counter

def crosswordPuzzle(crossword, words):
    words = words.split(';')   
    crossword = [list(row) for row in crossword]

    def can_place_h(r, c, word):
        if c + len(word) > 10: return False
        if c > 0 and crossword[r][c-1] != '+': return False
        if c + len(word) < 10 and crossword[r][c+len(word)] != '+': return False
        for i in range(len(word)):
            if crossword[r][c+i] not in ('-', word[i]):
                return False
        return True
        
    def can_place_v(r, c, word):
        if r + len(word) > 10: return False
        if r > 0 and crossword[r-1][c] != '+': return False
        if r + len(word) < 10 and crossword[r+len(word)][c] != '+': return False
        for i in range(len(word)):
            if crossword[r+i][c] not in ('-', word[i]):
                return False
        return True

    def place_horizontal(r, c, word):
        placed = [] 
        for i in range(len(word)):
            if crossword[r][c+i] == '-':
                crossword[r][c+i] = word[i]
                placed.append((r, c+i))
        return placed

    def place_vertical(r, c, word):
        placed = [] 
        for i in range(len(word)):
            if crossword[r+i][c] == '-':
                crossword[r+i][c] = word[i]
                placed.append((r+i, c))
        return placed

    def unplace(placed):
        for i, j in placed:
            crossword[i][j] = '-'

    def solve(index):     
        if index == len(words):
            return True
        word = words[index]
        for r in range(10):
            for c in range(10):
                if can_place_h(r, c, word):
                    placed = place_horizontal(r, c, word)
                    if solve(index+1): return True
                    unplace(placed)
                if can_place_v(r, c, word):
                    placed = place_vertical(r, c, word)
                    if solve(index+1): return True
                    unplace(placed)
        return False

    solve(0)
    return [''.join(row) for row in crossword]
```