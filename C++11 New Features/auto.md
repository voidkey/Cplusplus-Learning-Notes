For variables, specifies that the type of the variable that is being declared will be automatically deduced from its initializer.

### Explanation  
A placeholder type specifier may appear in the following contexts:

- in the type specifier of a variable: auto x = expr;. The type is deduced from the initializer.
If the placeholder type specifier is auto or type-constraint auto (since C++20), the variable type is deduced from the initializer using the rules for template argument deduction from a function call (see template argument deduction#Other contexts for details).
For example, given const auto& i = expr;, the type of i is exactly the type of the argument u in an imaginary template template<class U> void f(const U& u) if the function call f(expr) was compiled. Therefore, auto&& may be deduced either as an lvalue reference or rvalue reference according to the initializer, which is used in range-based for loop.
If the placeholder type specifier is decltype(auto) or type-constraint decltype(auto) (since C++20), the deduced type is decltype(expr), where expr is the initializer.

(since C++14)
If the placeholder type specifier is used to declare multiple variables, the deduced types must match. For example, the declaration auto i = 0, d = 0.0; is ill-formed, while the declaration auto i = 0, *p = &i; is well-formed and the auto is deduced as int.

- in the type-id of a new expression. The type is deduced from the initializer. For new T init (where T contains a placeholder type, init is either a parenthesized initializer or a brace-enclosed initializer list), the type of T is deduced as if for variable x in the invented declaration T x init;.
- (since C++14) in the return type of a function or lambda expression: auto& f();. The return type is deduced from the operand of its non-discarded (since C++17) return statement.
See function#Return_type_deduction.
- (since C++17) in the parameter declaration of a non-type template parameter: template<auto I> struct A;. Its type is deduced from the corresponding argument.
```C++
#include <iostream>
#include <utility>
 
template<class T, class U>
auto add(T t, U u) { return t + u; } // the return type is the type of operator+(T, U)
 
// perfect forwarding of a function call must use decltype(auto)
// in case the function it calls returns by reference
template<class F, class... Args>
decltype(auto) PerfectForward(F fun, Args&&... args) 
{ 
    return fun(std::forward<Args>(args)...); 
}
 
template<auto n> // C++17 auto parameter declaration
auto f() -> std::pair<decltype(n), decltype(n)> // auto can't deduce from brace-init-list
{
    return {n, n};
}
 
int main()
{
    auto a = 1 + 2;            // type of a is int
    auto b = add(1, 1.2);      // type of b is double
    static_assert(std::is_same_v<decltype(a), int>);
    static_assert(std::is_same_v<decltype(b), double>);
 
    auto c0 = a;             // type of c0 is int, holding a copy of a
    decltype(auto) c1 = a;   // type of c1 is int, holding a copy of a
    decltype(auto) c2 = (a); // type of c2 is int&, an alias of a
    std::cout << "a, before modification through c2 = " << a << '\n';
    ++c2;
    std::cout << "a, after modification through c2 = " << a << '\n';
 
    auto [v, w] = f<0>(); //structured binding declaration
 
    auto d = {1, 2}; // OK: type of d is std::initializer_list<int>
    auto n = {5};    // OK: type of n is std::initializer_list<int>
//  auto e{1, 2};    // Error as of C++17, std::initializer_list<int> before
    auto m{5};       // OK: type of m is int as of C++17, initializer_list<int> before
//  decltype(auto) z = { 1, 2 } // Error: {1, 2} is not an expression
 
    // auto is commonly used for unnamed types such as the types of lambda expressions
    auto lambda = [](int x) { return x + 3; };
 
//  auto int x; // valid C++98, error as of C++11
//  auto x;     // valid C, error in C++
}
```
