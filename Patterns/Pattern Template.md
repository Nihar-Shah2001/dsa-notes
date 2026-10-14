---
type: pattern
title: <% tp.file.title %>
tags:
  - dsa-pattern
category: "<% tp.system.suggester(["Array/String", "Search", "Tree/Graph", "DP/Recursion", "Data Structure Design", "Math/Bit"], ["Array/String", "Search", "Tree/Graph", "DP/Recursion", "Data Structure Design", "Math/Bit"]) %>"
date_created: <% tp.date.now("YYYY-MM-DD") %>
mastery: "<% tp.system.suggester(["Learning", "Comfortable", "Confident", "Mastered"], ["Learning", "Comfortable", "Confident", "Mastered"]) %>"
---

# <% tp.file.title %>

## When to Use
<!-- The recognition cues — what in a problem statement should make you think of this pattern? -->
-
-

## Core Idea
<!-- Explain the pattern's mechanism in your own words, as if writing the "textbook" entry for it. -->


## Signal Keywords / Constraints
<!-- e.g. "sorted array", "contiguous subarray", "kth largest", "no extra space" -->
-

## Generic Template (C++)
```cpp
// Skeleton to adapt per-problem
class Solution {
public:

};
```

## Variants Within This Pattern
| Variant | Trigger | Notes |
|---|---|---|
|  |  |  |

## Common Pitfalls
-
-

## Complexity Cheatsheet
| Operation | Time | Space |
|---|---|---|
|  |  |  |

## Problems Solved Using This Pattern
```dataview
TABLE difficulty AS "Difficulty", status AS "Status", last_reviewed AS "Last Reviewed"
FROM #dsa
WHERE pattern = this.file.name
SORT difficulty ASC
```

## Problems Still Pending (Todo/Attempted)
```dataview
LIST
FROM #dsa
WHERE pattern = this.file.name AND (status = "Todo" OR status = "Attempted")
```

## Connections to Other Patterns
<!-- e.g. "Sliding Window is a specialization of Two Pointers when both pointers move forward" -->
-
