---
tags:
  - sequencecontainers
---
# Declaration and Initialization

```cpp
#include <seqcont>
using namespace std;

int main()
{
    // C++11 initializer list syntax:
    seqcon<T> seqContName1{value1, value2, value3, ...};
    std::seqcon<T> seqContName2(firstIterator, lastIterator); // Adds values  from first Iterator to before the lastIterator
    seqcon<T> seqContName3(seqContName1); // Initializes with the other container
    seqcon<T> seqContName4(size, value); // Initlizes the container with size and fills it up with value.
    const auto rg = {value1, value2, ...};
    seqcon<T> seqContName5(from_range, rg);
}
```

