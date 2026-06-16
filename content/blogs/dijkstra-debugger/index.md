---
title: "Dijkstra and SPFA visualisation"
date: 2026-06-12T12:00:00+02:00
draft: false
toc: false
images:
tags:
  - algos
---

Dijkstra is easier to understand when you can watch the distances, queue, and visited set change step by step.
Here is the implementation of SPFA:

{{< highlight python >}}
def shortest_path(graph: list[list[tuple[int, int]]], a: int, b: int) -> int:
    def bfs(root: int, target: int):
        queue = deque([root])
        distance = [inf] * len(graph)
        distance[root] = 0
        while len(queue) > 0:
            node = queue.popleft()
            for neighbor, weight in graph[node]:
                if distance[neighbor] <= distance[node] + weight:
                    continue
                queue.append(neighbor)
                distance[neighbor] = distance[node] + weight
        return distance[target]
    r = bfs(a, b)
    return -1 if r == inf else r
{{< / highlight >}}

SPFA looks similar to BFS: it keeps nodes in a queue and relaxes their outgoing edges. The difference is that we do not mark a node as permanently visited. Instead, we only care whether we found a better distance to that node. If the distance improves, we put the node back into the queue so its neighbors can be checked again.

The cost of this approach is repeated work. SPFA can process a node before its best distance is known. In the example below, SPFA follows **B** and adds its neighbors to the queue, even though those paths will later be improved through **C**. That means nodes like **D** may be processed once with a worse distance, then processed again after a better path is discovered.

Dijkstra avoids much of this wasted work by always expanding the node with the smallest tentative distance first. When a node is popped from the priority queue, its shortest distance is final. At that point, we can safely use it to improve its neighbors without needing to revisit it later.

Use the debugger below step by step and watch these variables:

- `current`: the node popped from the priority queue
- `neighbor`: the node currently being inspected
- `alt`: the candidate distance through `current`
- `visited`: nodes whose shortest distance is already fixed
- `pq`: queued nodes with tentative distances
- `prev`: pointers used to rebuild the shortest path

{{< dijkstra-debugger >}}
