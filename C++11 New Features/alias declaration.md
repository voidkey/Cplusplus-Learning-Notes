How C++ ‘using’ or alias-declaration is better than typedef?  
*Alias-declaration or type-alias with 'using' statement offers a more flexible way to define type aliases than typedef, mainly because of alias templates.*
## Overview
Defining type aliases or synonyms with typedef has always been an indispensable part of writing a good quality C++ code. 
To outline how type aliases can help create more maintainable code, let's take an example of a simple banking application where a user can have multiple accounts. 
The following code declares two account types: Checking and Savings. An STL map collection is used to store the list of user accounts keyed by the int user identifier:  

```C++
class CheckingAccount;
class SavingsAccount;

// Map of UserId -> List of CheckingAccount
std::map<int, std::vector<CheckingAccount>> UserCheckingAccounts;
// Map of UserId -> List of SavingsAccount
std::map<int, std::vector<SavingsAccount>> UserSavingsAccounts;
```

## Alias-Declaration
Since C++11, the using statement can be used instead of typedef to define type synonyms. 
This new method of defining type aliases is known as alias-declaration or type-alias. 
The synonyms of user identifier and account collection types with alias-declaration can be defined as follows:  
using UserId = int;
using UserCheckingAccounts_t = std::map<UserId, std::vector<CheckingAccount>>;
using UserSavingsAccounts_t = std::map<UserId, std::vector<SavingsAccount>>;
Note that, the alias-declaration definitions look like variable declarations, which improves the readability. 
The improvement-in-readability argument is more persuasive when we compare the following function pointer alias definitions:
```C++
typedef void(*FP)(int);
  // vs
using FP = void(*)(int);

// FP can be used to declare a function pointer
void foo(FP callback);
```
Like function pointer declaration, another exotic and a rather lesser-known declaration is of reference to an array. With array references, functions can take array parameters without decaying them to pointers. The below code shows an example of defining array-reference alias and using that as a function parameter. Note that how the array reference parameter allows us to use a range-based loop:
```C++
// create an alias of reference to int[4];
using IntArray4 = int(&)[4];

// or with typedef
// typedef int(&IntArray4)[4];

// Use the array reference alias as parameter type
void foo(IntArray4 array) {
  // range-based loop on the array
  for(int i : array) std::cout << i << " ";
}

// foo can be called on a int[4] as:
int arr[4] = {6,7,8,9};
foo(arr); // logs  6 7 8 9
```
Readability is required, but it might not be a compelling reason for some to ditch typedef in favor of alias-declaration. 
However, alias-declarations have another feature, alias templates, which make them hard to overlook.
