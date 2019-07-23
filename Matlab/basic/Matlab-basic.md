[TOC levels=1-3]: #

# Table of Contents
- [Table of Contents](#table-of-contents)
- [Name](#name)
- [Purpose](#purpose)
- [Language fundamentals](#language-fundamentals)
  - [Entering commands](#entering-commands)
    - [Format output](#format-output)
    - [Continue long statements on multiple lines](#continue-long-statements-on-multiple-lines)
  - [Matrices and Arrays](#matrices-and-arrays)
    - [Creating, concatenating, and expanding matrices](#creating-concatenating-and-expanding-matrices)
    - [Array indexing](#array-indexing)
    - [Removing rows or columns from a matrix](#removing-rows-or-columns-from-a-matrix)
    - [Multidimensional Arrays](#multidimensional-arrays)
  - [Data types](#data-types)
    - [Special data types in Matlab](#special-data-types-in-matlab)
    - [Data type transforming](#data-type-transforming)
    - [Regular expression](#regular-expression)
  - [Operators and elementary operations](#operators-and-elementary-operations)
  - [Loops and conditional statements](#loops-and-conditional-statements)
- [Data import and analysis](#data-import-and-analysis)
- [Programming](#programming)

# Name
Matlab Basic: note file of the basic knowledge of the Matlab

# Purpose
This is the note file of the Matlab language, for learning and the future review. The original material comes from the [official website](https://www.mathworks.com/help/matlab/index.html?s_tid=CRUX_lftnav)

# Language fundamentals
The part is about the fundamental language information of Matlab.

## Entering commands
As you work in MATLAB®, you can enter individual statements in the Command Window. Therefore, the most basic knowledge of the Matlab is the different commands. The following examples are essential for daily usage.

| Command |                  Meaning                 |
|:-------:|:----------------------------------------:|
|   ans   |            Most recent answer            |
|   clc   |           Clear Command Window           |
|  format | Set Command Window output display format |
|   home  |             Send cursor home             |
|   more  |  Control paged output in Command Window  |

### Format output 
```Matlab
format loose % keeps the display of blank lines(default)
format compact % suppresses the display of blank lines

format short % numeric display(4 digit, default)
format short e % numeric display(4 digit plus e)
format long % numeric display(15 digit)
format + % all +
```

### Continue long statements on multiple lines
- This example shows how to continue a statement to the next line using ellipsis (...).
```Matlab
s = 1 - 1/2 + 1/3 - 1/4 + 1/5 ...
      - 1/6 + 1/7 - 1/8 + 1/9;
```
- Build a long character vector by concatenating shorter vectors together:
```Matlab
mytext = ['Accelerating the pace of ' ...
    'engineering and science'];
```

- The start and end quotation marks for a character vector must appear on the same line. For example, this code returns an error, because each line contains only one quotation mark:
```Matlab
mytext = 'Accelerating the pace of ... 
            engineering and science'
```

## Matrices and Arrays
### Creating, concatenating, and expanding matrices
- MATLAB has many functions that help create matrices with certain values or a particular structure. For example, the zeros and ones functions create matrices of all zeros or all ones. The first and second arguments of these functions are the number of rows and number of columns of the matrix, respectively.
```Matlab
A = zeros(3, 2) % A = 3 * 2 matrix all 0
B = ones(2, 4)
```

- You can also use square brackets to join existing matrices together. This way of creating a matrix is called concatenation. For example, concatenate two row vectors to make an even longer row vector.
```Matlab
A = ones(1,4);
B = zeros(1,4);
C = [A B]
%C = 1×8
 %    1     1     1     1     0     0     0     0
```

- The colon is a handy way to create matrices whose elements are sequential and evenly spaced. For example, create a row vector whose elements are the integers from 1 to 10.
```Matlab
A = 1:10
%A = 1×10
 %    1     2     3     4     5     6     7     8     9    10
```
- You can use the colon operator to create a sequence of numbers within any range, incremented by one.
```Matlab
A = -2.5:2.5
%A = 1×6
%-2.5000   -1.5000   -0.5000    0.5000    1.5000    2.5000
```
- To change the value of the sequence increment, specify the increment value in between the starting and ending range values, separated by colons.
```Matlab
A = 0:2:10
%A = 1×6
% 0     2     4     6     8    10
```
- An empty array in MATLAB is an array with at least one dimension length equal to zero. Empty arrays are useful for representing the concept of "nothing" programmatically. For example, suppose you want to find all elements of a vector that are less than 0, but there are none. The find function returns an empty vector of indices, indicating that it couldn't find any elements less than 0.
```Matlab
A = [1 2 3 4];
ind = find(A<0)
%ind =
%1x0 empty double row vector
```
### Array indexing
- The most common way is to explicitly specify the indices of the elements. For example, to access a single element of a matrix, specify the row number followed by the column number of the element.
```Matlab
A = [1 2 3 4; 5 6 7 8; 9 10 11 12; 13 14 15 16]
%A = 4×4

 %    1     2     3     4
 %    5     6     7     8
 %    9    10    11    12
 %   13    14    15    16

e = A(3,2)
%e = 10
```

- You can also reference multiple elements at a time by specifying their indices in a vector. For example, access the first and third elements of the second row of A.
```Matlab
r = A(2,[1 3])
%r = 1×2

   %  5     7
```
- To access elements in a range of rows or columns, use the colon. For example, access the elements in the first through third row and the second through fourth column of A.
```Matlab
r = A(1:3,2:4)
%r = 3×3

 %    2     3     4
 %    6     7     8
 %   10    11    12
```

- An alternative way to compute r is to use the keyword end to specify the second column through the last column. This approach lets you specify the last column without knowing exactly how many columns are in A.
```Matlab
r = A(1:3,2:end)
%r = 3×3

 %    2     3     4
 %    6     7     8
 %   10    11    12
```
- If you want to access all of the rows or columns, use the colon operator by itself. For example, return the entire third column of A.
```Matlab
r = A(:,3)
%r = 4×1

 %    3
 %    7
 %   11
 %   15
```
- Another method for accessing elements of an array is to use only a single index, regardless of the size or dimensions of the array. This method is known as linear indexing. While MATLAB displays arrays according to their defined sizes and shapes, they are actually stored in memory as a single column of elements. A good way to visualize this concept is with a matrix. While the following array is displayed as a 3-by-3 matrix, MATLAB stores it as a single column made up of the columns of A appended one after the other. The stored vector contains the sequence of elements 12, 45, 33, 36, 29, 25, 91, 48, 11, and can be displayed using a single colon.
```Matlab
A = [12 36 91; 45 29 48; 33 25 11]
%A = 3×3

%    12    36    91
%    45    29    48
%    33    25    11

Alinear = A(:)
%Alinear = 9×1

 %   12
 %   45
 %   33
 %   36
 %   29
 %   25
 %   91
 %   48
 %   11
```

### Removing rows or columns from a matrix

- The easiest way to remove a row or column of a matrix is setting that row or column equal to a pair of empty square brackets []. For example, create a 4-by-4 matrix and remove the second row.
```Matlab
A = magic(4)
%A = 4×4

 %   16     2     3    13
 %    5    11    10     8
 %    9     7     6    12
 %    4    14    15     1
```
```Matlab
A(2,:) = []
%A = 3×4

 %   16     2     3    13
 %    9     7     6    12
 %    4    14    15     1
```

- Now remove the third column.
```Matlab
A(:,3) = []
%A = 3×3

 %   16     2    13
 %    9     7    12
 %    4    14     1
```
### Multidimensional Arrays
Find [here](https://www.mathworks.com/help/matlab/math/multidimensional-arrays.html).

## Data types
By default, MATLAB® stores all numeric variables as double-precision floating-point values. Additional data types store text, integer or single-precision values, or a combination of related data in a single variable. 

### Special data types in Matlab 

### Data type transforming

### Regular expression 


## Operators and elementary operations

## Loops and conditional statements



# Data import and analysis


# Programming