Arithmetic types can be divided into two categories: integeral types(including boolean, character and integer types) and floating types.
## Boolean type
Value: true or false (1 or 0).
The minimum size is not defined.
## Character types
C++ provided several character types, most of them support internationlization. The basic character type is **char**, one **char** is the same size as one byte.  
Ohter character types are used to extend character set, like wchar_t, char16_t, char32_t. **wchar_t** type is used to ensure that any character in the maximum extended character set of the machine can be stored. **char16_t** and **char32_t** servered Unicode character set.
## Integer types
![integer types & their properties](assets/integer_types&their_properties.png)  
Besides the minimal bit counts, the C++ Standard guarantees that:
- **1 == sizeof(char) <= sizeof(short) <= sizeof(int) <= sizeof(long) <= sizeof(long long)**
## Floating types
floating types can be further divided into three categories:  
**1. Real floating types**
- float
- double 
- long double
**2. Complex floating types**
- float complex 
- double complex 
- long double complex
**3. Imaginary floating types**
- float imaginary 
- double imaginary
- long double imaginary
The latter two need to include <complex.h>. They are generally not used, so just know them.
## Range of value
![range_of_value](assets/range_of_value.png)
- **Note:** actual (as opposed to guaranteed minimal) ranges are available in the library headers <limits.h> and <float.h>

Reference from *https://en.cppreference.com/w/c/language/arithmetic_types* and *C++ Primer中文版：第5版*
