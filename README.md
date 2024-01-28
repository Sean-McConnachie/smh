# cpp_match
Bringing a little bit of Rust to C++

I suffered from a missing `break;` today... This is my solution. 

```c++
#include <iostream>
#include <functional>
#include <random>

#define CASE(statement) [&]() { return (statement); }
#define DEFAULT true

template<typename F>
struct s_MatchCase {
    std::function<bool()> condition;
    std::function<F()> function;
};

template<typename F, size_t N>
F match(const s_MatchCase<F> (&match_case)[N]) {
    for (const auto &[cond, func]: match_case) {
        if (cond()) {
            return func();
        }
    }
}
```

I'll benchmark and check for optimizations some other time.