> constexpr - specifies that the value of a variable or function can appear in constant expressions

The constexpr specifier declares that it is possible to evaluate the value of the function or variable at compile time.  
Such variables and functions can then be used where only compile time constant expressions are allowed (provided that appropriate function arguments are given).  
A constexpr specifier used in an object declaration or non-static member function (until C++14) implies const.  
A constexpr specifier used in a function or static member variable (since C++17) declaration implies inline.  
If any declaration of a function or function template has a constexpr specifier, then every declaration must contain that specifier.  

A constexpr variable must satisfy the following requirements:
- its type must be a LiteralType.
- it must be immediately initialized
- the full-expression of its initialization, including all implicit conversions, constructors calls, etc, must be a constant expression
