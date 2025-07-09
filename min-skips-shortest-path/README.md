# Shortest Path with Limited Time and Skipped Edges

This project implements a graph algorithm to solve the following problem:

> Given a directed graph with `N` nodes and `M` weighted edges, a source node `s`, a destination node `t`, and a time budget `B`, determine the **minimum number of edges** that need to be **skipped** (i.e., treated as zero-cost) in order to reach node `t` from node `s` within the time limit `B`.

## Problem Description

Each edge `(u, v)` has an associated travel time `ℓᵢ`, and the traveler has the option to **skip the cost of a limited number of edges** (i.e., move through them in zero time). The goal is to reach from `s` to `t` in at most `B` total time, using the **fewest possible skips**.

### Input:
- `N` (number of cities/nodes)
- `M` (number of roads/edges)
- `s` (starting city)
- `t` (destination city)
- `B` (maximum allowed time)
- Then `M` lines of: `u v ℓᵢ` (a road from `u` to `v` taking `ℓᵢ` hours)

### Output:
- A single integer: the **minimum number of edge skips** needed to reach city `t` from `s` in at most `B` time. If it's not possible even with all edges skipped, output `-1`.

## Algorithm Overview

The solution combines two main ideas:

### 1. Layered Dijkstra's Algorithm
To account for edge skips, the graph is **layered** into `k+1` layers, where `k` is the number of allowed skips. Each node `v` appears in every layer `i = 0,...,k`, representing the state "I am at node `v` having used `i` skips".

For each edge `(u, v, w)`:
- If we **don't skip**, we add an edge from `u` in layer `i` to `v` in layer `i` with cost `w`
- If we **do skip**, and haven't used all skips, we add an edge from `u` in layer `i` to `v` in layer `i+1` with cost `0`

A modified Dijkstra’s algorithm is then run on this layered graph to compute the minimum time to reach `t` with up to `k` skips.

### 2. Binary Search over `k`
We use binary search to determine the **minimum number of skips `k`** such that the shortest path from `s` to `t` with at most `k` skips is **less than or equal to `B`**.

The search space is: k ∈ [0, N - 1]


For each value of `k`, the `isPossible(k)` function runs layered Dijkstra to check if it’s feasible to reach `t` from `s` within the time limit `B` using up to `k` skips.

This results in a **logarithmic search over the number of allowed skips**.

## Time Complexity
 O(logM(Nk_maxlog(Nk_max))) 
 where `k_max` is the maximum number of skips explored by binary search.