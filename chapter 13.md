## ARRAYS:  
The C language provides a capability that enables the user to design a
set of similar data types, called array.  

Note: all arrays make use of pointers internally.  

An array is a data structure, with collection of similar elements. These similar elements
could be all ints, or all floats, or all chars, etc. Usually, the array of
characters is called a ‘string’, whereas an array of ints or floats is called
simply an array. Remember that all elements of any given array must be
of the same type, i.e., we cannot have an array of 10 numbers, of which
5 are ints and 5 are floats.  
Syntax :  
 data_type name_of array[array_size];  // declaration  
 data_type name_of array[array_size] = { e1, e2, ....} // intialization  
 NOte: [] tells the compiler that we are dealing with an array. Also, Its optional to mention the size if we want to nitialize all our elements.
 In intialization, the no. of elements should be less than or equal to array size. 
 If initialized elements are less than array size, the other elements are assigned 0.  
 On no initialization, there would be random garbage values stored in them.  
 Note : the index of array elements start from 0.  
 Array provides us a contiguous block of memory  according to array size and data type.   
 #### Accessing, entering and reading the array elements:  
 we can refer to an array element with the notation: arr[i], where i is the index (position) of the element.  
 Note: the index starts from 0 till (array_size -1).  
 Let us consider a simple program to understand these :   
   
     
       
         
         #include<stdio.h>
         int main()
         {
         int n;
         scanf("%d",&n);
         int a[n];
         for(int i=0; i<n; i++)
         scanf("%d",&a[i]);  
         int sum = 0;
         for(int i=0; i<n; i++)
         {printf("%d",&a[i]); 
         sum = sum + a[i];
         printf("\n%d",sum);
         }
         }
         
         
 ### Array Elements in Memory :
 Consider the following array declaration:  
int arr[8] ;  
What happens in memory when we make this declaration? 32 bytes get
immediately reserved in memory, 4 bytes each for the 8 integers (under
TC/TC++ the array would occupy 16 bytes as each integer would occupy
2 bytes). And since the array is not being initialized, all eight values
present in it would be garbage values. This so happens because the
storage class of this array is assumed to be auto. If the storage class is
declared to be static, then all the array elements would have a default initial value as zero. Whatever be the initial values, all the array
elements would always be present in contiguous memory locations.  A visual representation:  
![image](https://user-images.githubusercontent.com/64036955/121796644-4b63d200-cc38-11eb-8efb-2cd68affd8fd.png)  
### Bound Checking:  
In C, there is no check to see if the subscript used for an array exceeds
the size of the array. Data entered with a subscript exceeding the array
size will simply be placed in memory outside the array; probably on top
of other data, or on the program itself. This will lead to unpredictable
results, to say the least, and there will be no error message to warn you
that you are going beyond the array size.  
consider the program:  
#include <stdio.h>  
int main( )
{  
int num[ 40 ], i ;  
for ( i = 0 ; i <= 100 ; i++ )  
num[ i ] = i ;  
return 0 ;  
}  


### Pointers and array:
let us first
learn some pointer arithmetic. Consider the following example:   
#include <stdio.h>  
int main( )  
{  
int i = 3, *x ;   
float j = 1.5, *y ;  
char k = 'c', *z ;  
printf ( "Value of i = %d\n", i ) ;  
printf ( "Value of j = %f\n", j ) ;   
printf ( "Value of k = %c\n", k ) ;  
x = &i ;  
y = &j ;  
z = &k ;  
printf ( "Original address in x = %u\n", x ) ;  
printf ( "Original address in y = %u\n", y ) ;  
printf ( "Original address in z = %u\n", z ) ;  
x++ ;  
y++ ;  
z++ ;  
printf ( "New address in x = %u\n", x ) ;  
printf ( "New address in y = %u\n", y ) ;  
printf ( "New address in z = %u\n", z ) ;  
return 0 ;  
}  
Output:  
Value of i = 3
Value of j = 1.500000
Value of k = c
Original address in x = 65524
Original address in y = 65520
Original address in z = 65519
New address in x = 65528
New address in y = 65524
New address in z = 65520  
### Operations on pointers:
   
   
   
   ![image](https://user-images.githubusercontent.com/64036955/121805850-a7474e80-cc6a-11eb-8a4c-c854a3099e78.png)   
addr( ptr + i ) = addr( ptr ) + [ sizeof( T ) * i ]     
![image](https://user-images.githubusercontent.com/64036955/121805931-1755d480-cc6b-11eb-9f6c-05e73195e61e.png)
![image](https://user-images.githubusercontent.com/64036955/121805958-410efb80-cc6b-11eb-8048-fcec74881bbe.png)


   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   
   ### Passing entire array to a function:  
   Consider the following example:   
   #include<stdio.h>  
void display ( int *, int ) ;  
int main( )  
{  
int num[ ] = { 24, 34, 12, 44, 56, 17 } ;  
dislpay ( &num[ 0 ], 6 ) ;  
return 0 ;  
}  
void display ( int *j, int n )  
{  
int i ;  
for ( i = 0 ; i <= n - 1 ; i++ )  
{  
printf ( "element = %d\n", *j ) ;  
j++ ; /* increment pointer to point to next element */  
}  
}  
 Here, the display( ) function is used to print out the array elements.
Note that the address of the zeroth element is being passed to the
display( ) function. The for loop is same as the one used in the earlier
program to access the array elements using pointers. Thus, just passing
the address of the zeroth element of the array to a function is as good as
passing the entire array to the function.It is also necessary to pass the
total number of elements in the array, otherwise the display( ) function
would not know when to terminate the for loop. Note that the address
of the zeroth element (many a time called the base address) can also be
passed by just passing the name of the array. Thus the following two are just same:  
display ( &num[ 0 ], 6 ) ;   
display ( num, 6 ) ;  

Note:  on mentioning the name of the array, we get its
base address. Thus, by saying *num, we would be able to refer to the
zeroth element of the array, on mentioning the name of the array, we get its
base address. Thus, by saying *num, we would be able to refer to the
zeroth element of the array, when num points to the array's base element.  
the following notations are same:  
num[ i ]    
*( num + i )  
*( i + num )  
i[ num ]  

