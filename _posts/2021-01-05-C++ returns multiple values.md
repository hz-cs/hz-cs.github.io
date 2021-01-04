---
title: 'C++ returns multiple values'
date: 2199-01-01
permalink: /posts/2021/01/blog-post-2/
tags:
  - Coding
  - C++
  - Snippet
---

New programmers are usually in the search of ways to return multiple values from a function. Unfortunately, C and C++ do not allow this directly. But fortunately, with a little bit of clever programming, we can easily achieve this.

Below are the methods to return multiple values from a function in C:

    By using pointers.
    By using structures.
    By using Arrays.

Example: Consider an example where the task is to find the greater and smaller of two distinct numbers. We could write multiple functions. The main problem is the trouble of calling more than one functions since we need to return multiple values and of course, having more number of lines of code to be typed. 

Returning multiple values Using pointers: Pass the argument with their address and make changes in their value using pointer. So that the values get changed into the original argument. 

// Modified program using pointers 
#include <stdio.h> 

// add is the short name for address 
void compare(int a, int b, int* add_great, int* add_small) 
{ 
	if (a > b) { 

		// a is stored in the address pointed 
		// by the pointer variable *add_great 
		*add_great = a; 
		*add_small = b; 
	} 
	else { 
		*add_great = b; 
		*add_small = a; 
	} 
} 

// Driver code 
int main() 
{ 
	int great, small, x, y; 

	printf("Enter two numbers: \n"); 
	scanf("%d%d", &x, &y); 

	// The last two arguments are passed 
	// by giving addresses of memory locations 
	compare(x, y, &great, &small); 
	printf("\nThe greater number is %d and the"
		"smaller number is %d", 
		great, small); 

	return 0; 
} 


 Output:

Enter two numbers: 
5 8
The greater number is 8 and the smaller number is 5

Returning multiple values using structures : As the structure is a user-defined datatype. The idea is to define a structure with two integer variables and store the greater and smaller values into those variable, then use the values of that structure. 

// Modified program using structures 
#include <stdio.h> 
struct greaterSmaller { 
	int greater, smaller; 
}; 

typedef struct greaterSmaller Struct; 

Struct findGreaterSmaller(int a, int b) 
{ 
	Struct s; 
	if (a > b) { 
		s.greater = a; 
		s.smaller = b; 
	} 
	else { 
		s.greater = b; 
		s.smaller = a; 
	} 

	return s; 
} 

// Driver code 
int main() 
{ 
	int x, y; 
	Struct result; 

	printf("Enter two numbers: \n"); 
	scanf("%d%d", &x, &y); 

	// The last two arguments are passed 
	// by giving addresses of memory locations 
	result = findGreaterSmaller(x, y); 
	printf("\nThe greater number is %d and the"
		"smaller number is %d", 
		result.greater, result.smaller); 

	return 0; 
} 

 Output:

Enter two numbers: 
5 8
The greater number is 8 and the smaller number is 5

Returning multiple values using an array (Works only when returned items are of same types): When an array is passed as an argument then its base address is passed to the function so whatever changes made to the copy of the array, it is changed in the original array.
Below is the program to return multiple values using array i.e. store greater value at arr[0] and smaller at arr[1].

// Modified program using array 
#include <stdio.h> 

// Store the greater element at 0th index 
void findGreaterSmaller(int a, int b, int arr[]) 
{ 

	// Store the greater element at 
	// 0th index of the array 
	if (a > b) { 
		arr[0] = a; 
		arr[1] = b; 
	} 
	else { 
		arr[0] = b; 
		arr[1] = a; 
	} 
} 

// Driver code 
int main() 
{ 
	int x, y; 
	int arr[2]; 

	printf("Enter two numbers: \n"); 
	scanf("%d%d", &x, &y); 

	findGreaterSmaller(x, y, arr); 

	printf("\nThe greater number is %d and the"
		"smaller number is %d", 
		arr[0], arr[1]); 

	return 0; 
} 


 Output:

Enter two numbers: 
5 8
The greater number is 8 and the smaller number is 5

C++ Only Methods

    Returning multiple values Using References: We use references in C++ to store returned values. 
    
// Modified program using References in C++ 
#include <stdio.h> 

void compare(int a, int b, int &add_great, int &add_small) 
{ 
	if (a > b) { 
		add_great = a; 
		add_small = b; 
	} 
	else { 
		add_great = b; 
		add_small = a; 
	} 
} 

// Driver code 
int main() 
{ 
	int great, small, x, y; 

	printf("Enter two numbers: \n"); 
	scanf("%d%d", &x, &y); 

	// The last two arguments are passed 
	// by giving addresses of memory locations 
	compare(x, y, great, small); 
	printf("\nThe greater number is %d and the"
		"smaller number is %d", 
		great, small); 

	return 0; 
} 

 Output:

Enter two numbers: 
5 8
The greater number is 8 and the smaller number is 5

Returning multiple values using Class and Object : The idea is similar to structures. We create a class with two integer variables and store the greater and smaller values into those variable, then use the values of that structure. 

// Modified program using class 
#include <stdio.h> 

class GreaterSmaller { 
public: 
	int greater, smaller; 
}; 

GreaterSmaller findGreaterSmaller(int a, int b) 
{ 
	GreaterSmaller s; 
	if (a > b) { 
		s.greater = a; 
		s.smaller = b; 
	} 
	else { 
		s.greater = b; 
		s.smaller = a; 
	} 

	return s; 
} 

// Driver code 
int main() 
{ 
	int x, y; 
	GreaterSmaller result; 

	printf("Enter two numbers: \n"); 
	scanf("%d%d", &x, &y); 

	// The last two arguments are passed 
	// by giving addresses of memory locations 
	result = findGreaterSmaller(x, y); 
	printf("\nThe greater number is %d and the"
		"smaller number is %d", 
		result.greater, result.smaller); 

	return 0; 
} 


 Output:

Enter two numbers: 
5 8
The greater number is 8 and the smaller number is 5


Returning multiple values using STL tuple : The idea is similar to structures. We create a tuple with two integer variables and return the tuple, and then inside main function we use tie function to assign values to min and max that is returned by the function. 

// Modified program using C++ STL tuple 
#include<iostream> 
#include<tuple> 

using namespace std; 

tuple <int, int> findGreaterSmaller(int a, int b) 
{ 
	if (a < b) { 
	return make_tuple(a, b); 
	} 
	else { 
	return make_tuple(b, a); 
	} 
} 

// Driver code 
int main() 
{ 
	int x = 5, y= 8; 
	int max, min; 
	tie(min, max) = findGreaterSmaller(x, y); 

	printf("The greater number is %d and the "
		"smaller number is %d", 
		max, min); 

	return 0; 
} 

 Output:

The greater number is 8 and the smaller number is 5



While C++ does not have an official way to return multiple values from a function, one can make use of the std::pair, std::tuple, or a local struct to return multiple values.

However, with the introduction of structured binding in C++17, the process is greatly simplified as the output parameters no longer need to be initialized.

Code

The following code snippet shows the way to return multiple values from a function using a local structure:

#include <iostream>
using namespace std;

auto foo() {
  struct retVals {        // Declare a local structure 
    int i1, i2;
    string str;
  };
  return retVals {10, 20, "Hi"}; // Return the local structure
}

int main() {
  auto [value1, value2, value3] = foo(); // structured binding declaration
  cout << value1 << ", " << value2 << ", " << value3 << endl;
}

Note the structured binding syntax on line 131313; there is no need to instantiate output values before calling the function. The datatypes are determined automatically.

The std::tuple can also be used to return multiple values in conjunction with structured binding. This is shown below:

#include <iostream>
#include <tuple>

using namespace std;

tuple<int, float, string> foo()
{
  return {128, 3.142, "Hello"};
}

int main()
{
  auto [value1, value2, value3] = foo();
  cout << value1 << ", " << value2 << ", " << value3 << endl;
}





