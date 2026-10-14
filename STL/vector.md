---
type: stl-concept
category: container
header: <vector>
topic: stl
subtopic: sequence
level: foundational
prerequisites:
  - "[[Complexity Analysis]]"
related_concepts:
  - "[[deque]]"
  - "[[array]]"
  - "[[list]]"
next_concept:
  - "[[Prefix Sum]]"
  - "[[Two Pointers - Opposite Ends]]"
tags:
  - stl
created: 2026-10-09
updated: 2026-10-09
---
# vector

## 1. What It Is
**One line:** A resizable array stored in contiguous memory, with fast access by index and fast appends at the end.

**Header:** `#include <vector>`

**Underlying structure:** a dynamic array. It keeps spare capacity and reallocates (usually doubling) when full.

**Ordered / unique / contiguous / random access:** insertion order kept, duplicates allowed, contiguous, random access.

## 2. When To Use It (and When Not To)
**Use it when:**
- You need indexed access and mostly add or remove at the end (the default container)
- You want cache-friendly iteration
- You need a dynamic 2D grid (`vector<vector<int>>`), adjacency lists or a DP table

**Avoid it when:**
- You insert or erase often in the middle or at the front (each costs O(n))
- You need stable references while the size changes (growth moves elements)

**Pick this over:** [[deque]] when you only add at the back; [[list]] almost always, since lists lose on cache behaviour.

## 3. Core Operations
| Operation | Syntax | Time | Notes |
|---|---|---|---|
| Construct | `vector<int> v(n, x);` `vector<int> v = {1,2,3};` | O(n) | `v(n)` zero-initialises; `vector<vector<int>> g(r, vector<int>(c, 0));` for a grid |
| Access | `v[i]`, `v.at(i)`, `v.front()`, `v.back()` | O(1) | `at` checks bounds and throws; `[]` does not |
| Insert at end | `v.push_back(x)`, `v.emplace_back(args)` | amortised O(1) | Occasional O(n) when it reallocates |
| Insert in middle | `v.insert(it, x)` | O(n) | Shifts later elements |
| Erase | `v.pop_back()`, `v.erase(it)` | O(1), O(n) | Erasing from the end is cheap, elsewhere shifts |
| Search | `find(v.begin(), v.end(), x)` | O(n) | On sorted data use `lower_bound` for O(log n) |
| Size / empty / clear | `v.size()`, `v.empty()`, `v.clear()` | O(1), O(1), O(n) | `size()` returns an unsigned type |
| Resize / reserve | `v.resize(k)`, `v.reserve(k)` | O(n) | `reserve` avoids repeated reallocation |
| Iterate | `for (int x : v)`, `for (auto it = v.begin(); it != v.end(); ++it)` | O(n) | |

Space: O(n), with up to roughly 2n capacity after growth.

## 4. Iterators and Invalidation
- **Iterator category:** random access (contiguous).
- **begin / end / rbegin / rend / cbegin / cend:** `begin()` points to the first element, `end()` one past the last; `rbegin/rend` walk backwards.
- **What invalidates iterators, pointers and references:**
  - Insert: all of them if it reallocates (size exceeds capacity); otherwise only those at or after the insert point.
  - Erase: those at or after the erased element.
  - Reallocation: every iterator, pointer and reference. Call `reserve` first if you hold any.

## 5. Usage Examples (C++)
```cpp
#include <bits/stdc++.h>
using namespace std;

int main() {
    vector<int> v = {5, 2, 9, 1};
    v.push_back(7);                       // {5,2,9,1,7}
    sort(v.begin(), v.end());             // {1,2,5,7,9}
    int pos = lower_bound(v.begin(), v.end(), 5) - v.begin();   // 2

    // typical interview / contest idioms
    vector<int> prefix(v.size() + 1, 0);
    for (size_t i = 0; i < v.size(); ++i) prefix[i + 1] = prefix[i] + v[i];

    v.erase(unique(v.begin(), v.end()), v.end());               // remove duplicates (sorted)
    reverse(v.begin(), v.end());
}
```

**Common idioms**
- Remove an element by value: `v.erase(remove(v.begin(), v.end(), x), v.end());`
- Fill: `vector<int> dp(n + 1, INT_MAX);`
- Copy: `vector<int> w = v;` (deep copy)
- Swap to free memory: `vector<int>().swap(v);`

## 6. Pitfalls
- `v.size() - 1` underflows when the vector is empty, because `size()` is unsigned. Cast or compare carefully (`(int)v.size() - 1`).
- Holding an iterator, pointer or reference across `push_back` or `insert`.
- `v[i]` out of range is undefined behaviour, not an exception.
- Erasing inside a range-based `for` loop.
- `vector<bool>` is a special bit-packed type, so `&v[i]` and some algorithms behave differently.
- Passing large vectors by value; take `const vector<int>&`.

## 7. Complexity Summary
| Task | Time | Why |
|---|---|---|
| Index access | O(1) | Contiguous memory |
| Append | amortised O(1) | Doubling spreads the reallocation cost |
| Insert or erase in the middle | O(n) | Elements shift |
| Sort | O(n log n) | `std::sort` |
| Find in sorted vector | O(log n) | `lower_bound` / `binary_search` |

## 8. Compared With Related Tools
| Tool | Strength | Weakness | Use when |
|---|---|---|---|
| [[deque]] | O(1) at both ends | Slower indexing, not contiguous | A queue-like structure or sliding window |
| [[array]] | No heap allocation | Fixed size | The size is known at compile time |
| [[list]] | O(1) insert with an iterator | No indexing, poor cache behaviour | Rarely; splicing nodes |

## 9. Where It Shows Up in Problems
| Pattern or problem | Why this tool | Link |
|---|---|---|
| [[Prefix Sum]] | Store running sums for range queries | |
| [[Two Pointers - Opposite Ends]] | Index from both ends | |
| [[Fixed Sliding Window]] | Window over the array | |
| Graph adjacency lists | `vector<vector<int>> adj(n)` | |

## 10. Reference
- cppreference: [std::vector](https://en.cppreference.com/w/cpp/container/vector)
- Container member function table (what each container supports):

![[stl-container-member-functions.png]]

**Concept links** (same as the properties above)
- **Prerequisites:** [[Complexity Analysis]]
- **Related concepts:** [[deque]], [[array]], [[list]]
- **Next concept:** [[Prefix Sum]], [[Two Pointers - Opposite Ends]]
- **Hub:** [[STL Map]]
