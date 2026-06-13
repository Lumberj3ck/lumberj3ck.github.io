---
title: "Dijkstra and SPFA visualisation"
date: 2026-06-12T12:00:00+02:00
draft: false
toc: false
images:
tags:
  - algos
---

Dijkstra is easier to understand when you can see the variables move.

The thing is that djikstra faster because it figures improvements faster and when we find improvements it means that probable worse paths which could have been traveled through the node are skipped entirely, while SPFA still goes through those dead paths (they anyways will be updated).
This is visible on representation bellow, where SPFA first follows node **B** neighbors, we vaste time on this one because all of that neighbors paths will be improved, but it is not yet best we would have to update them, however they have already been added into the queue, luckily for us it is only node **D**, but if graph was large enough we might have added more nodes and you can see where this goes. From that node **D** we updated paths to other neighbors, but again they are not final paths. And only now after all of that computations we come to node **C** which actually gives us improvement on neighbors, but we have to recalculate neighbors of **B** and **D** again, thus we add **B** into the queue again.

Use the debugger below step by step and watch these variables:

- `current`: the node popped from the priority queue
- `neighbor`: the node currently being inspected
- `alt`: the candidate distance through `current`
- `visited`: nodes whose shortest distance is already fixed
- `pq`: queued nodes with tentative distances
- `prev`: pointers used to rebuild the shortest path

{{< dijkstra-debugger >}}

