---
Pattern: Two Pointers
topics:
  - array
  - DP
subtopic: Two Pointers
level: Basic
prerequisites:
  - "[[Complexity Analysis]]"
related_concepts:
next_concept:
created:
updated:
tags:
---
# Problem Statement
Given the array, you want to find the maximum difference i.e. `numbers[j] - numbers[i]` where `j > i`.
> **Input:** Array of `numbers`.
> **Output:** Return _the maximum running difference, else return `0`.

> [!Example] Example
> Input: `numbers = [7,1,5,3,6,4]`
> Output: 5
> Explanation: The difference `numbers[4] - numbers[1] = 6 - 1 = 5` .
## Clarifying questions to ask
1. What is the length of the array? - to get to know the range of input helps deciding the complexity.
2. What is the maximum `numbers[i]` could be? - to set up the datatype of array
3. What should be returned if no positive difference exists? - Here: `0`.
4. Does `j` have to be strictly greater than `i`? In other words, must the first element occur before the second?
## Constraints
> [!check] Constraints
> - `1 <= numbers.length <= 10^5`
> - `0 <= numbers[i] <= 10^4`
> 
> Since the length of array is `10^5` the time complexity cannot be `O(n^2)`.

> [!Example] Example
>Input:
>Output:
>Explanation:

# Optimal Approach:

> [!Info] Algorithm
> Maintain two variables:
> - `maxDifference` → maximum difference found so far.
> - `minValue` → minimum value encountered so far.
> For every `price`:
>	1. Calculate the difference between `number` and `minValue`.
>	2. Update `maxDifference`.
>	3. Update `minValue`.

> [!NOTE] Correctness Explanation 
> **Invariant**
> After processing the first `k` elements:
> `minValue` is the minimum value among the first `k` elements. Therefore, when processing `numbers[j]`, `numbers[j] - min_price` represents the maximum possible difference where `numbers[j]` is the second element. Since we evaluate this for every `j`, `max_profit` becomes the maximum valid difference over all pairs `(i, j)` satisfying `i < j`.
> Mathematical Approach: We want
$$
maxDifference = \max_{0\leq i < j < n} numbers[j] - numbers[i]
$$
For a fixed `j`, maximizing `numbers[j] - numbers[i]` is equivalent to minimizing `numbers[i]`i.e.
$$
maxDifferenceTillNow = \max_{j>i} (numbers[j] - numbers[i]) = numbers[j] - \min_{i} numbers[i]
$$
Hence, `numbers[i]` must be the `minValue` till now. Therefore, while scanning from left to right, we only need to remember minimum value seen so far (`minValue`). Then, for the current value `numbers[j]`:
$$
maxDifferenceTillNow = numbers[j] - minValue
$$
and we keep the maximum such difference. So we don't need to remember every previous element. We only need the minimum previous element. Thus, for every `j`, the algorithm considers the best possible difference ending at `j`.
Taking the maximum over all `j` gives:
$$
\max_{j>i}​(numbers[j]−numbers[i]) = \max_{j}(numbers[j]-\min_{i<j}numbers[i])
$$
Therefore, the algorithm is correct. This gives us an `O(n)` algorithm.
## Pattern Recognition
> [!Important] Key Takeaway
> When I see ... I should think ...
> Checklist:
> 1. 
# Code:
```c++
#include <algorithm>
#include <climits>
#include <vector>

using namespace std;

int maxProfit(vector<int>& numbers)
{
	int minValue = INT_MAX, maxDifference = 0;
	
	for(int number: numbers){
		maxDifference = max(maxDifference, number - minValue);
		minValue = min(minValue, number);
	}
	
	return maxDifference;
}
```
## Complexity Analysis:
> [!Note] Complexity
> Time Complexity: `O(n)` - single pass, one comparison + one update per element
> Space Complexity: `O(1)` - two scalar variables regardless of input size

> [!Warning] Edge Cases
> - Monotonically decreasing array (e.g., `[9,7,5,3,1]`) → no valid `j > i` gives a positive difference → returns 0.
> - Duplicate Values (All equal elements): (e.g., `[4,4,4]`) → `max` stays 0. Correct, since `numbers[i]==numbers[j]` gives 0.
> - Single-element array → loop runs once, `max_difference` stays 0, `min_value` updates.
> - Empty array (if constraints ever allow it) → returns 0 safely since `max_difference` never updates.
> - Minimum occurs late: `[5,4,3,2,10]` Here, the best difference is `10 - 2 = 8`.
# Dry Run:
> [!Example] Example
> **Input:** `numbers = [7,1,5,3,6,4]`
> 
|i|number|max_difference (before)|number - min_value|max_difference (after)|min_value (after)|
|---|---|---|---|---|---|
|0|7|0|7 - INT_MAX (skip, negative)|0|7|
|1|1|0|1 - 7 = -6|0|1|
|2|5|0|5 - 1 = 4|4|1|
|3|3|4|3 - 1 = 2|4|1|
|4|6|4|6 - 1 = 5|5|1|
|5|4|5|4 - 1 = 3|5|1|
Output: `maxDifference = 5`.
## Possible Mistakes

> [!Bug] Brute Force
> For every possible pair `(i, j)` where `j > i`, calculate:
$$
numbers[j] - numbers[i]
$$
and maintain the maximum.
	Algorithm:
	1. Iterate over every possible buying index `i`.
	2. For every `i`, iterate over every selling index `j > i`.
	3. Calculate `numbers[j] - numbers[i]`.
	4. Keep the maximum difference.
	Time: `O(n²)`, Space: `O(1)`. Since `n <= 10^5`, `O(n²)` is too expensive.
	Therefore, we need an `O(n)` solution. Checking every `(i, j)` pair gives `O(n²)`which is unnecessary.
# Related Problems/ Variants
- [ ] [Best Time to Buy and Sell Stock - LeetCode](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/?envType=study-plan-v2&envId=top-interview-150)