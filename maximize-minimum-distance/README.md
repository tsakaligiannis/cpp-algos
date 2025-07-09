# Problem: Maximize Minimum Distance

## Description
Given a set of non-overlapping intervals on the number line and an integer N, place N points such that the minimum distance between any two is as large as possible.

## Approach
Uses binary search to find the largest feasible minimum distance and a greedy algorithm to place the points.

## Input Format
- M: number of intervals
- Each interval: [s_i, f_i]
- N: number of points to place

## Output
The largest possible minimum distance between any two (consecutive) points.

## Example
Input:
5 3
5 9
0 3
12 12

Output:
3