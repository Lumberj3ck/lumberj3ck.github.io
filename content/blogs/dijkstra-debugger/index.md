---
title: "Dijkstra Debugger"
date: 2026-06-12T12:00:00+02:00
draft: false
toc: false
images:
tags:
  - algos
---

Dijkstra is easier to understand when you can see the variables move.

The key idea is simple: always expand the unvisited node with the smallest known distance. When we inspect an edge, we calculate a candidate distance. If it is better than the current value, we update `dist`, remember the previous node in `prev`, and push the node into the priority queue.

Use the debugger below step by step and watch these variables:

- `current`: the node popped from the priority queue
- `neighbor`: the node currently being inspected
- `alt`: the candidate distance through `current`
- `visited`: nodes whose shortest distance is already fixed
- `pq`: queued nodes with tentative distances
- `prev`: pointers used to rebuild the shortest path

{{< dijkstra-debugger >}}

The important moment is the relaxation check:

```python
alt = dist[current] + weight(current, neighbor)

if alt < dist[neighbor]:
    dist[neighbor] = alt
    prev[neighbor] = current
    push(priority_queue, (alt, neighbor))
```

Once a node is marked as visited, Dijkstra will not find a shorter route to it later. That works because all edge weights are non-negative, so the priority queue always gives us the next safest node to finalize.
