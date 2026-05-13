# The Torchbearer

**Student Name:** Chris Palomares
**Student ID:** 132809778
**Course:** CS 460 – Algorithms | Spring 2026

---

## Part 1: Problem Analysis

- **Why a single shortest-path run from S is not enough:**
  Running Dijkstra from S only tells us the cheapest way to get from the start node to every other node. It does not figure out the best order to visit all of the relic chambers, and different orders can lead to very different total fuel costs.

- **What decision remains after all inter-location costs are known:**
  Even after finding the cheapest distances between all important locations, we still have to decide the order to collect the relics. Some orders are much cheaper overall than others so the algorithm still has to compare different possibilities.

- **Why this requires a search over orders (one sentence):**
  The total fuel cost depends on the order the relics are visited, so the algorithm has to search through different relic orderings to find the minimum route.

---

## Part 2: Precomputation Design

### Part 2a: Source Selection

| Source Node Type | Why it is a source |
|---|---|
| Spawn node  | The Torchbearer starts here, so the algorithm needs shortest path costs from this node to every important location  |
| Relic nodes | The algorithm needs shortest path costs betweeen relic chambers so it can compare different possible collection orders. |

### Part 2b: Distance Storage

| Property | Your answer |
|---|---|
| Data structure name | Nested ductionary called dist_table |
| What the keys represent | The outer key is the source node and the inner key is the destination node |
| What the values represent | The minimum fuel cost from one node to another |
| Lookup time complexity | O(1) |
| Why O(1) lookup is possible | Python dictionaries use hash tables, so values can be accessed directly using keys |

### Part 2c: Precomputation Complexity

- **Number of Dijkstra runs:** k + 1 runs where k is the number of relics
- **Cost per run:** 0((V + E) log V)
- **Total complexity:** O((k + 1) (V + E) log V)
- **Justification (one line):** The algorithm runs Dijkstra once from the spawn node and once from each relic node so all important shortest path costs are precomputed

---

## Part 3: Algorithm Correctness

### Part 3a: What the Invariant Means

- **For nodes already finalized (in S):**
  Once a node is finalized, its distance is the true shortest distance from the source. The algorithm will not need to improve that node again.

- **For nodes not yet finalized (not in S):**
  For nodes still outside the finalized set, dist stores the best distance found so far using paths that only go through already finalized nodes.

### Part 3b: Why Each Phase Holds

- **Initialization : why the invariant holds before iteration 1:**
  Before the first loop, the source has distance 0 and every other node starts at infinity. This is correct because no paths have been explored yet.

- **Maintenance : why finalizing the min-dist node is always correct:**
  The algorithm always chooses the unfinished node with the smallest current distance. Because all edge weights are nonnegatieve, no later path through another unfinished node can make it cheaper.

- **Termination : what the invariant guarantees when the algorithm ends:**
  When the algorithm terminates, all nodes are finalized and their distances are correct. Unreachable nodes remain at infinity.

### Part 3c: Why This Matters for the Route Planner

The route planner needs correct shortest path distances so it can compare relic orders using accurate fuel costs

---

## Part 4: Search Design

### Why Greedy Fails

> State the failure mode. Then give a concrete counter-example using specific node names
> or costs (you may use the illustration example from the spec). Three to five bullets.

- **The failure mode:** _Your answer here._
- **Counter-example setup:** _Your answer here._
- **What greedy picks:** _Your answer here._
- **What optimal picks:** _Your answer here._
- **Why greedy loses:** _Your answer here._

### What the Algorithm Must Explore

> One bullet. Must use the word "order."

- _Your answer here._

---

## Part 5: State and Search Space

### Part 5a: State Representation

> Document the three components of your search state as a table.
> Variable names here must match exactly what you use in torchbearer.py.

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | | | |
| Relics already collected | | | |
| Fuel cost so far | | | |

### Part 5b: Data Structure for Visited Relics

> Fill in the table.

| Property | Your answer |
|---|---|
| Data structure chosen | |
| Operation: check if relic already collected | Time complexity: |
| Operation: mark a relic as collected | Time complexity: |
| Operation: unmark a relic (backtrack) | Time complexity: |
| Why this structure fits | |

### Part 5c: Worst-Case Search Space

> Two bullets.

- **Worst-case number of orders considered:** _Your answer (in terms of k)._
- **Why:** _One-line justification._

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

> Three bullets.

- **What is tracked:** _Your answer here._
- **When it is used:** _Your answer here._
- **What it allows the algorithm to skip:** _Your answer here._

### Part 6b: Lower Bound Estimation

> Three bullets.

- **What information is available at the current state:** _Your answer here._
- **What the lower bound accounts for:** _Your answer here._
- **Why it never overestimates:** _Your answer here._

### Part 6c: Pruning Correctness

> One to two bullets. Explain why pruning is safe.

- _Your answer here._

---

## References

> Bullet list. If none beyond lecture notes, write that.

- _Your references here._
