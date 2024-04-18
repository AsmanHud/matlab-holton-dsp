# Matlab related notes on Chapter 1.

## Basic operations on sequences

### Flip
There are several ways to flip a sequence in Matlab:
```matlab
x = [1 2 3 4];
y = x(end:-1:1)          % 1
% y = 4 3 2 1
y = x(length(x):-1:1)    % 2
y = fliplr(x)            % 3
y = flipud([1; 2; 3; 4]) % 4
```
[^1] While playing around with different methods to achieve the same result can be fun, sticking to the simplest solution (the first one) often proves to be the best strategy. This approach maintains readability of the code ('self-documenting' code), and also increases the portability to other platforms (using the basic set of Matlab functions).

[^1]: I found somewhat weird that in Matlab this `x(start:step:end)` is the syntax for the slice operation on a sequence, because I was used to `x[start:end:step]` from Python.

### Time decimation
Definition: `y[n] = x[nD]`
In Matlab, we just index every Dth point:
```matlab
x = [1 2 3 4 5 6 7 8];
D = 3;
y = x(1:D:end)
% y = 1 4 7
```

### Time expansion
Definition: `y[n] = x[n/U]` for n = 0, ±U, ±2U..., else y[n] = 0. This is due to the fact that evaluation of the expression above is not defined at fractional indices (for example U = 2, y[1] = x[1/2]). We want y[n] to be defined at every n, so we set the undefined values to 0s.
In Matlab, we can first create a zero-array, and then populate it with data:
```matlab
x = [1 2 3 4];
U = 2;
y = zeros(1, U*length(x));
y(1:U:end) = x;
y
% y = 1 0 2 0 3 0 4 0
```

### Operation on multiple sequences
Arithmetic operations on arrays in Matlab (like addition, subtraction, multiplication) are __vectorized__ meaning that performing the operation between two arrays automatically applies the operation element-wise.
```matlab
x1 = [1, 2, 3, 4];
x2 = [-1, 0, 1, 2];
ys = x1 + x2   %  0 2 4 6
yd = x1 - x2   %  2 2 2 2
yp = x1 .* x2  % -1 0 3 8
% default behavior of * operation is matrix mult.
% so instead we use the .* pointwise mult. operator
```

## Basic sequences

### Unit step
To implement a unit step, we can create a simple function[^2]:
```matlab
n = -2:2;  % -2 1 0 1 2
u(n)       %  0 0 1 1 1

function x = u(n)
    x = double(n >= 0);
end
```
This checks if the input time indice `n` is greater than or equal to zero or not, and the boolean value is casted to a number (0 or 1) by the `double()` method. So it will return 0 for n < 0, and 1 for n >= 0, which is the definition of a unit step sequence.

We can also define and use an anonymous function:
```matlab
u = @(n) double(n >= 0);

n = -2:2;  % -2 1 0 1 2
u(n)       %  0 0 1 1 1
```

[^2]: At the time of writing this, I was using Matlab R2023a, and before R2024a, you must had to define local functions at the end of the file. That's why you see a test case first, then the function definition, which looks odd to me

#### Use of the unit step as a switch
We can use the unit step function to "switch on" or "switch off" another function x[n]:
```
y[n] = x[n]u[n] = x[n] if n >= 0 else 0
```
In Matlab:
```matlab
u = @(n) double(n >= 0);

x = -2:2        % -2 -1 0 1 2
y = x .* u(x)   %  0  0 0 1 2
```

## Systems

### Shift
There is a trick to perform the shift operation in Matlab, as shifting might mean padding the array with zeros on either side, depending on the sign of the shift:
```matlab
x = [-1 2 0 5 3];
n = 1;
y = [zeros(1, n) x zeros(1, -n)]
y
%    0    -1     2     0     5     3
```
When we pass a negative argument to zeros(), it just returns an empty array, so we can dynamically pad the left or the right of the sequence with zeros based on the sign of shift.