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
  - [Data types](#data-types)
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


## Data types

## Operators and elementary operations

## Loops and conditional statements



# Data import and analysis


# Programming