---
type: pattern
topic: arrays
subtopic: running-aggregate
level: foundational
prerequisites:
  - "[[Complexity Analysis]]"
related_concepts:
  - "[[Kadane's Algorithm]]"
  - "[[Prefix Sum]]"
next_concept:
  - "[[Kadane's Algorithm]]"
  - "[[State Machine DP]]"
tags:
  - pattern
  - topic/arrays
created: 2026-10-09
updated: 2026-10-09
---
# Running Minimum

## 1. Problem Statement
**Problem:** Maximum Running Difference (the same idea as [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/), LeetCode)

**In my words:** Find the largest value of `numbers[j] - numbers[i]` where `j > i`. If every such difference is zero or negative, return 0.

**Input:** an integer array `numbers` with 1 ≤ n ≤ 10^5 and 0 ≤ numbers[i] ≤ 10^4.

**Output:** one integer, the maximum difference (0 if none is positive).

**Walkthrough of a small example**
```
Input:  [7, 1, 5, 3, 6, 4]
Output: 5
```
Why this output, step by step:
1. The smallest value that comes before 6 is 1 (index 1).
2. 6 (index 4) minus 1 (index 1) is 5.
3. No other later-minus-earlier pair gives more than 5.

## 2. Clarifying Questions
| Question to ask | Answer | What it settles |
|---|---|---|
| How long can the array be, and how large can values get? | n up to 10^5, values up to 10^4 | O(n²) is too slow, so aim for O(n); `int` is enough |
| What if no positive difference exists? | Return 0 | Start the answer at 0, not `INT_MIN` |
| Must `j` be strictly after `i`? | Yes | The minimum may only come from earlier elements |
| Can the array be empty or contain negatives? | Not under these constraints | Guard anyway if the constraints change |
| May I modify the input? | Not needed | One pass, no changes |

### Constraints
- 1 ≤ n ≤ 10^5
- 0 ≤ numbers[i] ≤ 10^4
- Target: O(n) time, O(1) extra space

## 3. Edge Cases
- [x] Strictly decreasing `[9, 7, 5, 3, 1]`: all differences negative, answer 0
- [x] All equal `[4, 4, 4]`: answer 0
- [x] Single element: answer 0
- [x] Minimum appears late `[5, 4, 3, 2, 10]`: answer 10 − 2 = 8
- [x] Extreme values: `INT_MAX` as the starting minimum must not be subtracted from
- [x] Empty array (if ever allowed): the loop never runs, answer 0

## 4. Optimal Approach
**Key insight:** for a fixed `j`, `numbers[j] - numbers[i]` is largest when `numbers[i]` is as small as possible. So the only thing worth remembering about the past is its minimum.

### Algorithm
1. Set `minValue` to a very large number and `maxDifference` to 0.
2. For each `number` from left to right:
   1. If at least one earlier element exists, set `maxDifference = max(maxDifference, number - minValue)`.
   2. Set `minValue = min(minValue, number)`.
3. Return `maxDifference`.

### Pseudocode
```
function maxRunningDifference(numbers):
    minValue = +infinity
    best = 0
    for each x in numbers:
        if minValue != +infinity:
            best = max(best, x - minValue)
        minValue = min(minValue, x)
    return best
```

### Why it works (proof of correctness)
- **Invariant:** after processing the first k elements, `minValue` is the minimum of those k elements and `maxDifference` is the best valid difference (never below 0) among them.
- **Initialisation:** with k = 0, `minValue` is infinity and `maxDifference` is 0, which is correct for an empty prefix.
- **Maintenance:** element k+1 can only form new pairs as the later element. Its best earlier partner is the smallest earlier value, which is `minValue` by the invariant, so the best new difference is `x - minValue`. Taking the max with the old `maxDifference` keeps the invariant, and `minValue` is then updated to include x.
- **Termination:** after n elements `maxDifference` is the best over all pairs.
- **Why nothing better is missed:** max over i<j of (a[j] − a[i]) = max over j of (a[j] − min over i<j of a[i]). For each j we pick the best possible i, so no pair can beat the result.

## 5. Code (C++)
```cpp
#include <algorithm>
#include <climits>
#include <vector>
using namespace std;

int maxRunningDifference(const vector<int>& numbers) {
    int minValue = INT_MAX, maxDifference = 0;
    for (int number : numbers) {
        if (minValue != INT_MAX)                       // skip the first element's comparison
            maxDifference = max(maxDifference, number - minValue);
        minValue = min(minValue, number);
    }
    return maxDifference;
}
```
The `INT_MAX` guard avoids `number - INT_MAX` overflowing if negative values are ever allowed. Starting `minValue` at the first element and looping from index 1 is an equivalent alternative.

## 6. Complexity
| | Cost | Why |
|---|---|---|
| Time | O(n) | One pass, one comparison and one update per element |
| Space | O(1) | Two integer variables |

## 7. Dry Run
Input: `[7, 1, 5, 3, 6, 4]`

| Step | Current element | State before (min, best) | What happens | State after (min, best) |
|---|---|---|---|---|
| 1 | 7 | (∞, 0) | no earlier element, min becomes 7 | (7, 0) |
| 2 | 1 | (7, 0) | 1 − 7 = −6, best stays 0; min becomes 1 | (1, 0) |
| 3 | 5 | (1, 0) | 5 − 1 = 4, best becomes 4 | (1, 4) |
| 4 | 3 | (1, 4) | 3 − 1 = 2, best stays 4 | (1, 4) |
| 5 | 6 | (1, 4) | 6 − 1 = 5, best becomes 5 | (1, 5) |
| 6 | 4 | (1, 5) | 4 − 1 = 3, best stays 5 | (1, 5) |

Answer: 5

## 8. Brute Force and Bugs
**Brute force:**
- Idea: try every pair (i, j) with j > i and keep the largest difference.
- Time / space: O(n²) / O(1).
- Why the constraints rule it out: with n = 10^5 that is about 5 × 10^9 pair checks, far above the roughly 10^8 operations a second budget.

**Bugs I made or could make:**
- Updating `minValue` before computing the difference, which allows `i = j` (harmless here, wrong in variants needing strict `i < j`)
- Starting `maxDifference` at `INT_MIN` and returning a negative number when 0 is required
- Taking the global min and max of the array, which ignores the later-minus-earlier order
- Skipping the constraints check and writing the O(n²) version first

## 9. Related Problems
| Problem | Platform / sheet | Link | Difficulty | What is different |
|---|---|---|---|---|
| Best Time to Buy and Sell Stock | LeetCode 121 (LeetCode 150, NeetCode 150, Blind 75, Grind 75) | [link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/) | Easy | The same problem with prices |
| Best Time to Buy and Sell Stock II | LeetCode 122 (LeetCode 150) | [link](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/) | Medium | Unlimited transactions, so add every positive step |
| Maximum Subarray | LeetCode 53 | [link](https://leetcode.com/problems/maximum-subarray/) | Medium | The running aggregate becomes the best sum ending here |
| InterviewBit, Fraz, Striver A2Z, GeeksforGeeks, Apna College | see the tracker | | | Add the exact problems from each sheet as you solve them |

## 10. Variants
| Variant or closely related concept | How it differs |
|---|---|
| [[Kadane's Algorithm]] | Also one pass, but tracks the best sum of a subarray ending at each position |
| [[Prefix Sum]] | Summarises the past as a sum for range queries instead of a min or max |
| [[State Machine DP]] | Stock problems with several transactions or cooldowns need states, not one minimum |

**Concept links** (same as the properties above)
- **Prerequisites:** [[Complexity Analysis]]
- **Related concepts:** [[Kadane's Algorithm]], [[Prefix Sum]]
- **Next concept:** [[Kadane's Algorithm]], [[State Machine DP]]
- **Hub:** [[Map of Patterns]]
