# Development Log – The Torchbearer

**Student Name:** Chris Palomares
**Student ID:** 132809778
---

## Entry 1 – [Date 5/8/2026]: Initial Plan

I started with reading through the ASSIGNMENT.md before starting anything so I could understand the project as a whole.
I noticed the problem is similar to the traveling Salesman style problem where the Torchbearer has to visit all relic nodes in the 
cheapest order possible in a weighted directed graph. My plan is to first use Dijkstra's algorithm to precompute shortest paths between
important nodes, and then I will use a backtracking search to test different relic orders while pruning expensive paths early.
I think the pruning section will probably be the hardest part because a bad lower bound could accidentally remove the optimal
solution. I also plan to test each function separately before combining everything together.

---

## Entry 2 – [5/12/2026]: [Dijkstra Implementation and Debugging]


I started with working on implementing Dijkstra's algorithm and the distance precomputation table. I then ran into a bug
where my code was not precompute_distance was running correctly and this was due to me accidently running 
sources - select_sources(spawn, relics, exit_node) instead of sources = select_sources(spawn, relics, exit_node). Having the
minus sign vs the equal sign was causing the function to fail. After fixing that mistake, the distance table started storing shortest path
results correctly for the spawn node and relic nodes. I also tested the algorithm on smaller graphs first to make sure
path costs were being calculated correctly before moving on to the recursive search portion.

---

## Entry 3 – [5/12/2026]: [Correctness and Search Design]

I started with reveiwing how Dijkstra's invariant guarantees that finalized nodes always have the true shortest path distance.
At first I was confused about why the minimum distance node could safely be finalized immediately, but after reviewing the rolel of 
nonnegative edge weights I was able to make more sense of it. I also started working on the search design section and realized that a greedy strategy
of always taking the closest relic does no always produce the minimum total route cost. So I decided the final solution would need a recursive 
search that explores different relic collection orders.

---

## Entry 4 – [Date]: Post-Implementation Reflection

> Required. Written after your implementation is complete. Describe what you would
> change or improve given more time.

_Your entry here._

---

## Final Entry – [Date]: Time Estimate

> Required. Estimate minutes spent per part. Honesty is expected; accuracy is not graded.

| Part | Estimated Hours |
|---|---|
| Part 1: Problem Analysis | |
| Part 2: Precomputation Design | |
| Part 3: Algorithm Correctness | |
| Part 4: Search Design | |
| Part 5: State and Search Space | |
| Part 6: Pruning | |
| Part 7: Implementation | |
| README and DEVLOG writing | |
| **Total** | |
