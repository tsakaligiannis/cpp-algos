# Minimizing Hazardous Interaction Cost

This project solves a **combinatorial optimization** problem involving the **segmentation of interacting items** to minimize total pairwise interaction cost.

---

## Problem Definition

Given **N items**, we must group them into **K containers (segments)** such that:

- Items are placed **in order** across containers.
- Each container can hold any number of items (including 1).
- For every pair of items `(i, j)` in the same container (with `i < j`), there is an added cost of `A[i][j]`.
- The **total cost** is the sum of all such pairwise interactions within each container.

**Goal:** Partition the `N` substances into `K` consecutive segments to **minimize** the **total energy cost**.

---

## Input Format

- Two integers `N` and `K`: number of substances and number of containers.
- A triangular matrix of integers `A[i][j]` (`1 ≤ i < j ≤ N`), where `A[i][j]` represents the reaction energy between substance `i` and `j`.

---

## Output

- A single integer: the **minimum total energy** that can be produced from valid placement of substances into `K` containers.

---

## Constraints

1 ≤ K ≤ N ≤ 1500
0 ≤ A[i][j] ≤ 99


---

## Approach

We use **Dynamic Programming** with precomputed segment costs:

1. **Precompute Costs**:  
   For every interval `[i, j]`, compute the total cost of placing all substances `i` through `j` in the same container: 
   cost[i][j] = ∑A[x][y] for all i ≤ x < y ≤ j
2. **DP State**:  
Let `dp[k][n]` be the minimum energy needed to split the first `n` substances into `k` containers.
3. **Recurrence**:
dp[k][n] = min_{m ≤ n} (dp[k - 1][m] + cost[m+1][n])
4. **Base Case**:
dp[0][0] = 0 (zero items, zero containers = zero cost)

## Example

### Input:
3 2
3 2
4

### Output:
3

## Complexity:
**O(KN²)**