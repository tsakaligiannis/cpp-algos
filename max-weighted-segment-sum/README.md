# Maximum Weighted Segment Sum (C++)

This project implements a **dynamic programming** solution to an optimization problem involving partitioning a sequence into segments of bounded length to maximize a custom weighted sum.

## Problem Definition

Given a sequence of `N` non-negative integers `h(1), h(2), ..., h(N)` and a maximum segment length `K`, you are to partition the sequence into contiguous segments, each of length **at most `K`**.

The **value** of a segment from index `i` to `j` (`j - i + 1 ≤ K`) is defined as: (j - i + 1) × max{ h(i), h(i+1), ..., h(j) }


Your goal is to partition the sequence into valid segments such that the **sum of the segment values is maximized**.

## Input

- An integer `N` (number of elements), and `K` (maximum segment length)  
- A list of `N` integers: `h(1), h(2), ..., h(N)`, representing the value of each element

**Constraints:**

- `3 ≤ N ≤ 5 × 10⁴`
- `1 ≤ K ≤ 10³`
- `0 ≤ h(i) ≤ 10⁵`

## Output

Print a single integer — the maximum achievable sum according to the segmentation rule.

## Example

### Input
7 3
9 8 7 9 4 3 9


### Output
84

## Approach

This problem is solved using **Dynamic Programming (DP)**.

- Let `dp[i]` be the maximum value achievable using the first `i` elements.
- For each position `i`, iterate back up to `K` elements, maintaining the max value in that window, and update `dp[i]` accordingly.
- Recurrence relation:  dp[i] = max_{1 ≤ j ≤ K} (dp[i - j] + j × max(h[i-j], ..., h[i-1]))
- Base case: dp[0]=0

**Time Complexity:**  
`O(N × K)`
