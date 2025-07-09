# Problem: Spanning Tree with Maximum Profit-to-Weight Ratio

## Description

Given an undirected, connected graph with `N` nodes and `M` edges, each edge offers:
- A **profit** `p(e)`
- A **weight** `w(e)`

The goal is to construct a **spanning tree** `T` such that the **ratio** of total profit to total weight:

P(T) / W(T) = (∑ p(e)) / (∑ w(e))

is **maximized**.

This is a bi-objective optimization problem, requiring a spanning tree that balances high profit with low weight.

---

## Input Format

- First line: two integers `N` and `M`
  - `N`: number of nodes (1 ≤ N ≤ 50,000)
  - `M`: number of edges (1 ≤ M ≤ 200,000)
- Next `M` lines: each line contains 4 integers `u`, `v`, `p`, `w`
  - `u`, `v`: endpoints of an edge
  - `p`: profit of the edge (0 ≤ p ≤ 200)
  - `w`: weight of the edge (0 < w ≤ 200)

---

## Output Format

Two integers `P` and `W`, such that:
- `P/W` is the maximum achievable **reduced fraction** of total profit over total weight for a spanning tree.

---

## Sample Input

4 5
1 2 2 1
2 3 3 2
3 4 1 1
4 1 2 2
1 3 1 3

## Sample Output
6 3


---

## Approach

The solution uses **parametric search** combined with **Kruskal’s algorithm**:

1. Define the ratio `λ = P(T)/W(T)` and search for the maximum feasible value using **binary search**.
2. For a fixed `λ`, define a new edge score: p(e) - λ * w(e)
and sort edges by this "modified profit".
3. Use **Kruskal’s algorithm** with a **greedy selection** based on this modified score to build a spanning tree.
4. If the resulting ratio is greater than `λ`, update your search range accordingly.
5. Finally, print the resulting `P/W` in **lowest terms**, using `gcd`.

---

## Complexity

- Time Complexity: `O(M log M * log (1/ε))` where `ε` is the precision of the binary search.
- Space Complexity: `O(N + M)`