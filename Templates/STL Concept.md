---
type: stl-concept
category:
header:
topic: stl
subtopic:
level:
prerequisites: []
related_concepts: []
next_concept: []
tags: [stl]
created: {{date:YYYY-MM-DD}}
updated: {{date:YYYY-MM-DD}}
---
<!--
Properties
category:          container | adaptor | iterator | algorithm | functor | utility
header:            the include, e.g. <vector>, <algorithm>, <iterator>
subtopic:          sequence | associative | unordered | adaptor | non-modifying | modifying | sorting | numeric | iterator-category | ...
level:             foundational | core | advanced
prerequisites / related_concepts / next_concept: link notes as "[[Note Name]]" so the graph connects STL notes with pattern notes
Use [[Pattern Name]] links to connect an STL tool to the patterns that rely on it (for example vector -> [[Prefix Sum]]).
-->
# {{title}}

## 1. What It Is
**One line:**

**Header:** `#include <>`

**Underlying structure:** (dynamic array, red-black tree, hash table, binary heap, ...)

**Ordered / unique / contiguous / random access:** 

## 2. When To Use It (and When Not To)
**Use it when:**
-

**Avoid it when:**
-

**Pick this over:** [[ ]] because ...

## 3. Core Operations
| Operation | Syntax | Time | Notes |
|---|---|---|---|
| Construct |  |  |  |
| Access |  |  |  |
| Insert |  |  |  |
| Erase |  |  |  |
| Search |  |  |  |
| Size / empty / clear |  |  |  |
| Iterate |  |  |  |

Space:

## 4. Iterators and Invalidation
- **Iterator category:** (input, forward, bidirectional, random access, contiguous)
- **begin / end / rbegin / rend / cbegin / cend:**
- **What invalidates iterators, pointers and references:**
  - Insert:
  - Erase:
  - Reallocation / rehash:

## 5. Usage Examples (C++)
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    // basic usage

    // typical interview / contest idiom
}
```

**Common idioms**
- 

## 6. Pitfalls
-

## 7. Complexity Summary
| Task | Time | Why |
|---|---|---|
|  |  |  |

## 8. Compared With Related Tools
| Tool | Strength | Weakness | Use when |
|---|---|---|---|
| [[ ]] |  |  |  |

## 9. Where It Shows Up in Problems
| Pattern or problem | Why this tool | Link |
|---|---|---|
| [[ ]] |  |  |

## 10. Reference
- cppreference: [{{title}}](https://en.cppreference.com/w/cpp/)
- Container member function table (what each container supports):

![[stl-container-member-functions.png]]

**Concept links** (same as the properties above)
- **Prerequisites:** [[ ]]
- **Related concepts:** [[ ]]
- **Next concept:** [[ ]]
- **Hub:** [[STL Map]]
