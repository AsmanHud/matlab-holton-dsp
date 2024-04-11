# Matlab related notes on Chapter 1.

## Flip
There are several ways to flip a sequence in Matlab:
```matlab
x = [1 2 3 4];
y = x(end:-1:1)          % 1[^1]
y = x(length(x):-1:1)    % 2
y = fliplr(x)            % 3
y = flipud([1; 2; 3; 4]) % 4
```
While playing around with different methods to achieve the same result can be fun, sticking to the simplest solution (the first one) often proves to be the best strategy. This approach maintains readability of the code ('self-documenting' code), and also increases the portability to other platforms (using the basic set of Matlab functions).
*A sidenote: the bracket syntax in Matlab is: x(end:step:start), which is kind of weird, but OK*
{:.sidenote}
[^1]: This is a sidenote, implemented as a footnote.