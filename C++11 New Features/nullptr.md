
//Definition of NULL in C
#define NULL (void*)0              
 
//Definition of NULL in C++
#ifndef NULL
#ifdef _cpluscplus                  
#define NULL 0                        
#else
#define NULL ((void*)0)            
#endif
#endif

nullptr is always a pointer type. 0 (aka. C's NULL bridged over into C++) could cause ambiguity in overloaded function resolution, among other things:

This problem falls into the following categories:

- Improve support for library building, by providing a way for users to write less ambiguous code, so that over time library writers will not need to worry about overloading on integral and pointer types.

- Improve support for generic programming, by making it easier to express both integer 0 and nullptr unambiguously.

- Make C++ easier to teach and learn.


**Here is Bjarne Stroustrup's wordings,**

> In C++, the definition of NULL is 0, so there is only an aesthetic difference. I prefer to avoid macros, so I use 0. Another problem with NULL is that people sometimes mistakenly believe that it is different from 0 and/or not an integer. In pre-standard code, NULL was/is sometimes defined to something unsuitable and therefore had/has to be avoided. That's less common these days.

If you have to name the null pointer, call it nullptr; that's what it's called in C++11. Then, "nullptr" will be a keyword.
