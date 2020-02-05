# Safe Comparison

## In a nutshell

*safe comparison* is a header only library that provides a type `is` which can be used for safe comparisons. The
current implementation covers `==, !=` and `in_range`. For details see _Example usage_.

## Inspiration

I got the inspiration from a talk by Björn Fahller _Modern Techniques for Keeping Your Code DRY_.

## Example usage

```cpp
#include <safe_comparison>

using namespace safe_comparison;

int main()
{
    constexpr int x = 2;
    constexpr int y = 3;
    constexpr int z = 4;

    if(is{x, y, z}.in_range(2, 5)) {
        // ...
    }

    static_assert(is{x, y, z}.in_range(2, 5), "x,y,z not in range of 2,3");
    static_assert(not is{x, y, z}.in_range(3, 5),
                  "x,y,z not in range of 2,3");
    static_assert(not is{x, y, z}.in_range(2, 3),
                  "x,y,z not in range of 2,3");


    constexpr int a = 1;
    constexpr int b = 1;
    constexpr int c = 1;

    if(is{x, y, z} == 1) {
        // ...
    }

    static_assert(is{a, b, c} == 1, "a,b,c are not all 1");
    static_assert(1 == is{a, b, c}, "a,b,c are not all 1");

    static_assert(not(is{a, b, c} == 0), "a,b,c are not all 1");
    static_assert(not(0 == is{a, b, c}), "a,b,c are not all 1");
}
```

## Include in your project

Put `safe_comparison` in the include path or your compiler or an existing include folder. The structure `is` is in the
namespace `safe_comparison`.
