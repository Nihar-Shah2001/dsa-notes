---
type: pattern
topic:
subtopic:
level:
prerequisites: []
related_concepts: []
next_concept: []
tags: [pattern]
created: {{date:YYYY-MM-DD}}
updated: {{date:YYYY-MM-DD}}
---
<!--
Properties
topic:             arrays | strings | binary-search | linked-list | stack-queue | backtracking | trees | heap | greedy-intervals | graphs | trie | dp | bits | math | advanced
level:             foundational | core | advanced
prerequisites:     notes to read first, e.g. ["[[Prefix Sum]]"]
related_concepts:  similar or combinable concepts, e.g. ["[[Kadane's Algorithm]]"]
next_concept:      what to learn after this, e.g. ["[[State Machine DP]]"]
Property links feed the graph view; the links in section 10 repeat them in the body so a published site (Quartz) draws the same graph.
-->
# {{title}}

## 1. Problem Statement
**Problem:** [Title (platform)](https://) <!-- paraphrase in your own words, link the original, never paste it -->

**In my words:**

**Input:**

**Output:**

**Walkthrough of a small example**
```
Input:
Output:
```
Why this output, step by step:
1.
2.

## 2. Clarifying Questions
| Question to ask | Answer | What it settles |
|---|---|---|
| How large can the input be, and what is the value range? |  | Target complexity and integer type |
| What should be returned when no valid answer exists? |  | Return value for the empty case |
| Can there be duplicates, negatives or an empty input? |  | Edge cases |
| Is the input sorted, or may I modify it? |  | Which approaches are allowed |
| Strict or non-strict comparison (`<` or `<=`)? |  | Off-by-one behaviour |

### Constraints
-

## 3. Edge Cases
- [ ] Empty or single element
- [ ] All elements equal / duplicates
- [ ] Already sorted / reverse sorted
- [ ] Extreme values (overflow, `INT_MIN`, `INT_MAX`)
- [ ] No valid answer
-

## 4. Optimal Approach
**Key insight:**


### Algorithm
1.
2.
3.

### Pseudocode
```
function solve(input):
    ...
```

### Why it works (proof of correctness)
- **Invariant:** after processing the first k items, ...
- **Initialisation:** the invariant holds before the first item because ...
- **Maintenance:** if it holds before item k, it holds after because ...
- **Termination:** at the end the invariant gives the answer because ...
- **Why nothing better is missed:** (exchange argument, or the property that lets us discard everything else)

## 5. Code (C++)
```cpp
#include <bits/stdc++.h>
using namespace std;

```

## 6. Complexity
| | Cost | Why |
|---|---|---|
| Time |  |  |
| Space |  |  |

## 7. Dry Run
Input:

| Step | Current element | State before | What happens | State after |
|---|---|---|---|---|
|  |  |  |  |  |

Answer:

## 8. Brute Force and Bugs
**Brute force:**
- Idea:
- Time / space:
- Why the constraints rule it out:

**Bugs I made or could make:**
-

## 9. Related Problems
| Problem | Platform / sheet | Link | Difficulty | What is different |
|---|---|---|---|---|
|  | LeetCode | [ ](https://) |  |  |
|  | InterviewBit | [ ](https://) |  |  |
|  | Striver A2Z | [ ](https://) |  |  |
|  | NeetCode / Blind / Grind | [ ](https://) |  |  |
|  | GeeksforGeeks | [ ](https://) |  |  |
|  | Apna College | [ ](https://) |  |  |
|  | Fraz | [ ](https://) |  |  |
|  | Codeforces / AtCoder / CSES | [ ](https://) |  |  |

## 10. Variants
| Variant or closely related concept | How it differs |
|---|---|
| [[ ]] |  |

**Concept links** (same as the properties above)
- **Prerequisites:** [[ ]]
- **Related concepts:** [[ ]]
- **Next concept:** [[ ]]
- **Hub:** [[Map of Patterns]]
