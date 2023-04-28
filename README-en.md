# Why is it a bad practice to use `using namespace std` in C++ ?  

## But it is faster for me!  

Is it realy faster to not type 5 characters ? Even me with my horrible finger placement on my keyboard I don't lose 1 second to write it, and the time you'll take to solve your problems with the `using namespace std` will be greater than the time you saved from not typing `std::`.

## Why does it exists if it is a bad practice?  

This line exists because before C++ didn't have namspaces so every function, class... of the standard library weren't in any namespace but when modern C++ arrived, namespaces were added to the language and everything in the standard library was moved to the namespace std. To make it easier for programmers to port their programs in modern C++ they added this line.

## Why is it a bad practice?  

Imagine you have two namespaces, `foo` and `bar` in your code :

```cpp
#include <iostream>

namespace foo {
    void foo() {
        std::cout << "foo" << std::endl;
    }
}

namespace bar {
    void bar() {
        std::cout << "bar" << std::endl;
    }
}

using namespace foo;
using namespace bar;

int main() {
    foo(); // displays "foo"
    bar(); // displays "bar"
}
```

in this code there is no problem but now imagine that you add a function foo in the namespace `bar`

```cpp
#include <iostream>

namespace foo {
  void foo() {
     std::cout << "foo" << std::endl;
  }
}

namespace bar {
  void foo() {
    std::cout << "foo but inside bar" << std::endl;
  }

  void bar() {
    std::cout << "bar" << std::endl;
  }
}

using namespace foo;
using namespace bar;

int main() {
  foo(); // ???
  foo(); // ???
  bar(); // displays "bar"
}
```

the compiler is not able to know which function you want to use but if you directly did 

```cpp
#include <iostream>

namespace foo {
  void foo() {
     std::cout << "foo" << std::endl;
  }
}

namespace bar {
  void foo() {
    std::cout << "foo but inside bar" << std::endl;
  }

  void bar() {
    std::cout << "bar" << std::endl;
  }
}

int main() {
  foo::foo(); // displays "foo"
  bar::foo(); // displays "foo but inside bar"
  bar::bar(); // displays "bar"
}
```

you don't have any problem and you don't have to take time to solve the problem with `using namespace`. This is why `using namespace std` is a bad practice.