https://docs.microsoft.com/en-us/cpp/cpp/decltype-cpp?view=vs-2019

Explanation
1) If the argument is an unparenthesized id-expression or an unparenthesized class member access expression, then decltype yields the type of the entity named by this expression. If there is no such entity, or if the argument names a set of overloaded functions, the program is ill-formed.
If the argument is an unparenthesized id-expression naming a structured binding, then decltype yields the referenced type (described in the specification of the structured binding declaration).

(since C++17)
If the argument is an unparenthesized id-expression naming a non-type template parameter, then decltype yields the type of the template parameter (after performing any necessary type deduction if the template parameter is declared with a placeholder type).

(since C++20)
2) If the argument is any other expression of type T, and
a) if the value category of expression is xvalue, then decltype yields T&&;
b) if the value category of expression is lvalue, then decltype yields T&;
c) if the value category of expression is prvalue, then decltype yields T.
If expression is a function call which returns a prvalue of class type or is a comma expression whose right operand is such a function call, a temporary object is not introduced for that prvalue.

(until C++17)
If expression is a prvalue other than a (possibly parenthesized) immediate invocation (since C++20), a temporary object is not materialized from that prvalue: such prvalue has no result object.

(since C++17)
The type need not be complete or have an available destructor, and can be abstract. This rule doesn't apply to sub-expressions: in decltype(f(g())), g() must have a complete type, but f() need not.
Note that if the name of an object is parenthesized, it is treated as an ordinary lvalue expression, thus decltype(x) and decltype((x)) are often different types.

decltype is useful when declaring types that are difficult or impossible to declare using standard notation, like lambda-related types or types that depend on template parameters.

```C++
#include <iostream>
 
struct A { double x; };
const A* a;
 
decltype(a->x) y;       // type of y is double (declared type)
decltype((a->x)) z = y; // type of z is const double& (lvalue expression)
 
template<typename T, typename U>
auto add(T t, U u) -> decltype(t + u) // return type depends on template parameters
                                      // return type can be deduced since C++14
{
    return t+u;
}
 
int main() 
{
    int i = 33;
    decltype(i) j = i * 2;
 
    std::cout << "i = " << i << ", "
              << "j = " << j << '\n';
 
    auto f = [](int a, int b) -> int
    {
        return a * b;
    };
 
    decltype(f) g = f; // the type of a lambda function is unique and unnamed
    i = f(2, 2);
    j = g(3, 3);
 
    std::cout << "i = " << i << ", "
              << "j = " << j << '\n';
}
```
