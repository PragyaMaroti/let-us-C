## Multi-Dimensional Arrays: 
### 2-D Arrays:  






#### Memory map of a 2-D array :
though we have visualized a 2-D array as a matrix, in rectangular shape, but in memory,
whether it is a one-dimensional or a two-dimensional array, the array
elements are stored in one continuous chain. For example:  
consider the 2-D array : s(4)(1);  
In memory, it is stored as:  
![image](https://user-images.githubusercontent.com/64036955/121806792-f1caca00-cc6e-11eb-9a28-2b0f08730971.png)  

The C language embodies an unusual but powerful capability—it can
treat parts of arrays as arrays. More specifically, each row of a twodimensional
array can be thought of as a one-dimensional array. This is a
very important fact if we wish to access array elements of a twodimensional
array using pointers. Thus, the declaration,
int s(5 )(2 ) ;
can be thought of as setting up an array of 5 elements, each of which is
a one-dimensional array containing 2 integers.  
More specifically,
s[ 0 ] gives the address of the zeroth one-dimensional array, s[ 1 ] gives
the address of the first one-dimensional array and so on.  
Consider the following program :  

   
      
      #include <stdio.h>  
      int main( )  
      {  
      int s[ 4 ] [2] = {  
      { 1234, 56 },
      { 1212, 33 },
      { 1434, 80 },
      { 1312, 78 }
      } ;
      int i ;
      for ( i = 0 ; i <= 3 ; i++ )
      printf ( "Address of %d th 1-D array = %u\n", i, s[ i ] ) ;
      return 0 ;
      }
And here is the output...
   
     Address of 0 th 1-D array = 65508
     Address of 1 th 1-D array = 65516
     Address of 2 th 1-D array = 65524
     Address of 3 th 1-D array = 65532
 Now, we have been able to reach each one-dimensional array. What
remains is to be able to refer to individual lements of a onedimensional
array. Suppose we want to refer to the element:
   
    s[ 2 ][ 1 ]
using pointers. We know (from the above program) that s[ 2 ] would
give the address 65524, the address of the second one-dimensional
array. Obviously ( 65524 + 1 ) would give the address 65528. Or ( s[ 2 ] +
1 ) would give the address 65528. And the value at this address can be
obtained by using the value at address operator, saying *( s[ 2 ] + 1 ).
But, we have already studied while learning one-dimensional arrays that
num[ i ] is same as *( num + i ). Similarly, *( s[ 2 ] + 1 ) is same as, *( *( s
+ 2 ) + 1 ). Thus, all the following expressions refer to the same element:
    
      s[ 2 ][ 1 ]
      * ( s[ 2 ] + 1 )
      * ( * ( s + 2 ) + 1 )

Let's see its implementation with the following program:  
    
       # include <stdio.h>
      int main( )
      {

      int s[ 4 ][ 2 ] = {
      { 1234, 56 },
      { 1212, 33 },
      { 1434, 80 },
      { 1312, 78 }
      } ;
      int i, j ;
      for ( i = 0 ; i <= 3 ; i++ )
      {
      for ( j = 0 ; j <= 1 ; j++ )
      printf ( "%d ", *( *( s + i ) + j ) ) ;
      printf ( "\n" ) ;
      }
      return 0 ;
      }
      
   And here is the output...
      
      
      1234 56
      1212 33
      1434 80
      1312 78  
      
   #### Pointer to an Array  
   Syntax:    

data_type (*var_name)[size_of_array];  
This way, we  declare a pointer that can point to whole array instead of only one element of the array. This pointer is useful when talking about multidimensional arrays.  
Example:  
int (*ptr)[10];
Here ptr is pointer that can point to an array of 10 integers. Since subscript have higher precedence than indirection, it is necessary to enclose the indirection operator and pointer name inside parentheses. Here the type of ptr is ‘pointer to an array of 10 integers’.  
Example to understand the difference betwwen pointer to the 0th alement and pointer to the whole array:  
  
   

    #include<stdio.h>

    int main()
    {
	// Pointer to an integer
	int *p;
	
	// Pointer to an array of 5 integers
	int (*ptr)[5];
	int arr[5];
	
	// Points to 0th element of the arr.
	p = arr;
	
	// Points to the whole array arr.
	ptr = &arr;
	
	printf("p = %p, ptr = %p\n", p, ptr);
	
	p++;
	ptr++;
	
	printf("p = %p, ptr = %p\n", p, ptr);
	
	return 0;
}

Here, The base type of p is int while base type of ptr is ‘an array of 5 integers’.  
When the pointer arithmetic is performed relative to the base size, so if we write ptr++, then the pointer ptr will be shifted forward by 20 bytes.  
But why should we use a pointer to an array to print elements of a 2-D
array. Is there any situation where we can appreciate its usage better?
The entity pointer to an array is immensely useful when we need to pass
a 2-D array to a function.  

### Passing 2-D Array to a Function: 
There are three ways in which we can pass a 2-D array to a function.
These are illustrated in the following program:  
   
   	/* Three ways of accessing a 2-D array */
	# include <stdio.h>
	void display ( int *q, int , int ) ;
	void print ( int q[ ][ 4 ], int , int ) ;
	int main( )
	{
	int a[ 3 ][ 4 ] = {
	1, 2, 3, 4,
	5, 6, 7, 8,
	9, 0, 1, 6
	} ;
	display ( a, 3, 4 ) ;
	show ( a, 3, 4 ) ;
	print ( a, 3, 4 ) ;
	return 0 ;
	}
	void display ( int *q, int row, int col )
	{
	int i, j ;
	for ( i = 0 ; i < row ; i++ )
	{
	for ( j = 0 ; j < col ; j++ )
	printf ( "%d ", * ( q + i * col + j ) ) ;
	printf ( "\n" ) ;
	}
	printf ("\n" ) ;
	}
	void show ( int ( *q )[ 4 ], int row, int col )
	{
	int i, j ;
	int *p ;
	for ( i = 0 ; i < row ; i++ )
	{void print ( int q[ ][ 4 ], int row, int col )
	{
	int i, j ;
	for ( i = 0 ; i < row ; i++ )
	{
	for ( j = 0 ; j < col ; j++ )
	printf ( "%d ", q[ i ][ j ] ) ;
	printf ( "\n" ) ;
	}
	printf ( "\n" ) ;
	}
	p = q + i ;
	for ( j = 0 ; j < col ; j++ )
	printf ( "%d ", * ( p + j ) ) ;
	printf ( "\n" ) ;
	}
	printf ( "\n" ) ;
	}
	void show ( int ( *q )[ 4 ], int, int ) ;
And here is the output…

		1 2 3 4
		5 6 7 8
		9 0 1 6
		1 2 3 4
		5 6 7 8
		9 0 1 6
		1 2 3 4
		5 6 7 8
		9 0 1 6
		
A more general formula for accessing each
array element would be:
* ( base address + row no. * no. of columns + column no. )  

In the show( ) function, we have defined q to be a pointer to an array of
4 integers through the declaration:
int ( *q )[ 4 ] ;
To begin with, q holds the base address of the zeroth 1-D array, i.e.
65502 (refer Figure 14.4). This address is then assigned to p, an int
pointer, and then using this pointer, all elements of the zeroth 1-D array
are accessed. Next time through the loop, when i takes a value 1, the
expression q + i fetches the address of the first 1-D array.  
In the third function print( ), the declaration of q looks like this:
int q[ ][ 4 ] ;
This is same as int ( *q )[ 4 ], where q is pointer to an array of 4
integers. The only advantage is that, we can now use the more familiar
expression q[ i ][ j ] to access array elements.  
### Array of Pointers:  
Since a pointer variable always
contains an address, an array of pointers would be nothing but a
collection of addresses. The addresses present in the array of pointers
can be addresses of isolated variables or addresses of array elements or
any other addresses. All rules that apply to an ordinary array apply to
the array of pointers as well.  
An array of pointers can even contain the addresses of other arrays. The
following program would justify this:  

	#include <stdio.h>
	int main( )
	{
	static int a[ ] = { 0, 1, 2, 3, 4 } ;
	int *p[ ] = { a, a + 1, a + 2, a + 3, a + 4 } ;
	Chapter 14: Multidimensional Arrays 279
	printf ( "%u %u %d\n", p, *p, * ( *p ) ) ;
	return 0;
	}
Extending this idea, We can hace __3-D array__ which can be seen as an array of 2-D array. It will have 3 [] and its elements can be accessed in similar manner :  
arr[ 2 ][ 3 ][ 1 ]
*( *( *( arr + 2 ) + 3 ) + 1 )  
Extending these concepts, we can even have an n-dimensional array, but 3 and above dimensions are rarely used in practise.
