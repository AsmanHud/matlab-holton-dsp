# Matlab related notes on Chapter 1.

## Flip
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

[^1]: I found somewhat weird that in Matlab we have x(start:step:end), because I mostly wrote code in Python, where we have x[start\:end\:step]

## Time decimation
Definition: `y[n] = x[nD]`
In Matlab, we just index every Dth point:
```matlab
x = [1 2 3 4 5 6 7 8];
D = 3;
y = x(1:D:end)
% y = 1 4 7
```

## Time expansion
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