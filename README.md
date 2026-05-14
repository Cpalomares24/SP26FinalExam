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

- **The failure mode:** A greedy strategy can choose the closest relic first but still end up with a more expensive total route

- **Counter-example setup:** Suppose S -> B costs 1, S -> C costs 2, B -> C costs 100, C -> B costs 1, B -> D costs 1, D -> C costs 1, and both C and B can reach T with costs 1.

- **What greedy picks:** A greedy algorithm would puck B first because it is the cheapest immediate choice from S.

- **What optimal picks:** The optimal solution may visit relics in a different order like S -> B -> D -> C -> T because the total cost is smaller overall.
- **Why greedy loses:** Greedy only looks at the next cheapest move and ignores how that choice affects future travel costs.

### What the Algorithm Must Explore

- The algorithm must explore diffrent relic collection orders to find the minimum total fuel cost.

---

## Part 5: State and Search Space

### Part 5a: State Representation

| Component | Variable name in code | Data type | Description |
|---|---|---|---|
| Current location | current_loc | node | Tracks where the Torchbearer currently is in the route |
| Relics already collected | relics_visited_order | list | Stores the relics already collected in the order they were visited |
| Fuel cost so far | cost_so_far | float/int | Tracks the total fuel used so far in the current route |

### Part 5b: Data Structure for Visited Relics

| Property | Your answer |
|---|---|
| Data structure chosen | set called relics_remaining |
| Operation: check if relic already collected | Time complexity: O(1) |
| Operation: mark a relic as collected | Time complexity: O(1) |
| Operation: unmark a relic (backtrack) | Time complexity: O(1) |
| Why this structure fits | A set is useful because relics can be removed and added back quickly during backtracking |

### Part 5c: Worst-Case Search Space

- **Worst-case number of orders considered:** k!
- **Why:** In the worst case, the algorithm may need to try every possible order of the k relics

---

## Part 6: Pruning

### Part 6a: Best-So-Far Tracking

- **What is tracked:** The algorithm tracks the cheapest complete route found so far using the best variable 
- **When it is used:** It is checked during recursion before exploring more branches
- **What it allows the algorithm to skip:** It allows the algorithm to skip routes that are already more expensive than the current best solution

### Part 6b: Lower Bound Estimation

- **What information is available at the current state:** The algorithm knows the current location, the fuel costs used so far, and which relics still remain
- **What the lower bound accounts for:** The lower bound uses the current fuel cost and the additional travel costs needed to continue the route
- **Why it never overestimates:** All edge weights are nonnegative, so adding more travel can never reduce the total route cost

### Part 6c: Pruning Correctness

- Pruning is safe because branches are only pruned when its current cost is already greater than or equal to the best complete route found so far
 Also since all remaining travel costs are nonnegative, continuing that branch cannot produce a cheaper final solution.

---

## References

- Used lecture notes, slides, and class textbook