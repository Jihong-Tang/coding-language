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
      - [Cell Arrays](#cell-arrays)
      - [Struture Arrays](#struture-arrays)
      - [Function Handles](#function-handles)
      - [Other special structure](#other-special-structure)
    - [Regular expression](#regular-expression)
  - [Operators and elementary operations](#operators-and-elementary-operations)
  - [Loops and conditional statements](#loops-and-conditional-statements)
- [Data import and analysis](#data-import-and-analysis)
  - [Data import and output](#data-import-and-output)
    - [Low-level File I/O](#low-level-file-io)
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
#### Cell Arrays
A [cell array](https://www.mathworks.com/help/matlab/cell-arrays.html?s_tid=CRUX_lftnav) is a data type with indexed data containers called cells, where each cell can contain any type of data. Cell arrays commonly contain either lists of character vectors of different lengths, or mixes of strings and numbers, or numeric arrays of different sizes. Refer to sets of cells by enclosing indices in smooth parentheses, (). Access the contents of cells by indexing with curly braces, {}.

- When you have data to put into a cell array, create the array using the cell array construction operator, {}.
```Matlab
myCell = {1, 2, 3;
          'text', rand(5,10,2), {11; 22; 33}}
%myCell = 2x3 cell array
 %   {[   1]}    {[          2]}    {[     3]}
 %   {'text'}    {5x10x2 double}    {3x1 cell}
```
- You also can use the {} operator to create an empty 0-by-0 cell array.
```Matlab
C = {}
%C =
%  0x0 empty cell array
```
- To add values to a cell array over time or in a loop, create an empty N-dimensional array using the cell function.
```Matlab
emptyCell = cell(3,4,2)
%emptyCell = 3x4x2 cell array
%emptyCell(:,:,1) = 

%    {0x0 double}    {0x0 double}    {0x0 double}    {0x0 double}
%    {0x0 double}    {0x0 double}    {0x0 double}    {0x0 double}
%    {0x0 double}    {0x0 double}    {0x0 double}    {0x0 double}


%emptyCell(:,:,2) = 

%    {0x0 double}    {0x0 double}    {0x0 double}    {0x0 double}
%    {0x0 double}    {0x0 double}    {0x0 double}    {0x0 double}
%    {0x0 double}    {0x0 double}    {0x0 double}    {0x0 double}
```
emptyCell is a 3-by-4-by-2 cell array, where each cell contains an empty array, [].

- Cell array indices in smooth parentheses refer to sets of cells. For example, to create a 2-by-2 cell array that is a subset of C, use smooth parentheses.
```Matlab
C = {'one', 'two', 'three'; 
     1, 2, 3}
%C = 2x3 cell array
%    {'one'}    {'two'}    {'three'}
%    {[  1]}    {[  2]}    {[    3]}
```
```Matlab
upperLeft = C(1:2,1:2)
%upperLeft = 2x2 cell array
%    {'one'}    {'two'}
%    {[  1]}    {[  2]}
```
- Access the contents of cells--the numbers, text, or other data within the cells--by indexing with curly braces. For example, to access the contents of the last cell of C, use curly braces.
```Matlab
last = C{2,3}
%last = 3
```
last is a numeric variable of type double, because the cell contains a double value.

- Similarly, you can index with curly braces to replace the contents of a cell.
```Matlab
C{2,3} = 300
%C = 2x3 cell array
%    {'first'}    {'second'}    {'third'}
%    {[    1]}    {[     2]}    {[  300]}
```

#### Struture Arrays
A structure array is a data type that groups related data using data containers called fields. Each field can contain any type of data. Access data in a structure using dot notation of the form structName.fieldName. For more information.

- Store a patient record in a scalar structure with fields name, billing, and test.
```Matlab
patient(1).name = 'John Doe';
patient(1).billing = 127.00;
patient(1).test = [79, 75, 73; 180, 178, 177.5; 220, 210, 205];
patient
%patient = struct with fields:
%       name: 'John Doe'
%    billing: 127
%       test: [3x3 double]
```

- Create scalar (1-by-1) structure arrays struct1 and struct2, each with fields a and b:
```Matlab
struct1.a = 'first';
struct1.b = [1,2,3];
struct2.a = 'second';
struct2.b = rand(5);
struct1,struct2
%struct1 = struct with fields:
%    a: 'first'
%    b: [1 2 3]

%struct2 = struct with fields:
%    a: 'second'
%    b: [5x5 double]
```    
Just as concatenating two scalar values such as [1,2] creates a 1-by-2 numeric array, concatenating struct1 and struct2 creates a 1-by-2 structure array.
```Matlab
combined = [struct1,struct2]
%combined = 1x2 struct array with fields:
%    a
%    b
```

#### Function Handles
A function handle is a data type that stores an association to a function. For example, you can use a function handle to construct anonymous functions or specify call back functions. Also, you can use a function handle to pass a function to another function, or call local functions from outside the main function.

- To create a handle for a function, precede the function name with an @ sign. For example, if you have a function called myfunction, create a handle named f as follows:
```Matlab
f = @myfunction;
```
- You call a function using a handle the same way you call the function directly. For example, suppose that you have a function named computeSquare, defined as:
```Matlab
function y = computeSquare(x)
y = x.^2;
end
```
- Create a handle and call the function to compute the square of four.
```Matlab
f = @computeSquare;
a = 4;
b = f(a)
%b =

 %   16
```
- If the function does not require any inputs, then you can call the function with empty parentheses, such as
```Matlab
h = @ones;
a = h()
%a =

%    1
```
- Without the parentheses, the assignment creates another function handle.
```Matlab
a = h
%a = 

   % @ones
```
- You can create handles to anonymous functions. An anonymous function is a one-line expression-based MATLAB function that does not require a program file. Construct a handle to an anonymous function by defining the body of the function, anonymous_function, and a comma-separated list of input arguments to the anonymous function, arglist. The syntax is:
```Matlab
h = @(arglist)anonymous_function
```
- For example, create a handle, sqr, to an anonymous function that computes the square of a number, and call the anonymous function using its handle.
```Matlab
sqr = @(n) n.^2;
x = sqr(3)
%x =

%    9
```

#### Other special structure
- [Categorical Arrays](https://www.mathworks.com/help/matlab/categorical-arrays.html?s_tid=CRUX_lftnav)
- [Timetables](https://www.mathworks.com/help/matlab/timetables.html?s_tid=CRUX_lftnav)
- [Map containers](https://www.mathworks.com/help/matlab/map-containers.html?s_tid=CRUX_lftnav)
- [Time series](https://www.mathworks.com/help/matlab/map-containers.html?s_tid=CRUX_lftnav)

### Regular expression 

|     Function    |                  Description                  |
|:---------------:|:---------------------------------------------:|
|      regexp     |            Match regular expression           |
|     regexpi     |    Match regular expression, ignoring case    |
|    regexprep    | Replace part of text using regular expression |
| regexptranslate |     Translate text into regular expression    |

 Syntax for `regexp`
- startIndex = regexp(str,expression)
- [startIndex,endIndex] = regexp(str,expression)
- out = regexp(str,expression,outkey)
- [out1,...,outN] = regexp(str,expression,outkey1,...,outkeyN)
- ___ = regexp(___,option1,...,optionM)
- ___ = regexp(___,'forceCellOutput')


## Operators and elementary operations
Similar to C++
## Loops and conditional statements
Similar to C++

# Data import and analysis
## Data import and output 
### Low-level File I/O
|  Function |                       Description                      |
|:---------:|:------------------------------------------------------:|
|   fclose  |               Close one or all open files              |
|    feof   |                Test for end of the file                |
|   ferror  |               File I/O error information               |
|   fgetl   |    Read line from file, removing newline characters    |
| filteread |              Read contents of file as text             |
|   fopen   |    Open file, or obtain information about open files   |
|  fprintf  |                 Write data to text file                |
|   fread   |               Read data from binary file               |
|  frewind  | Move file position indicator to beginning of open file |
|   fscanf  |                Read data from text file                |
|   fseek   |           Move to specified position in file           |
|   ftell   |                    Current position                    |
|   fwrite  |                Write data to binary file               |

# Programming
