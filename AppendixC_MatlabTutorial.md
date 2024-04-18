# Notes on Matlab Tutorial given in Appendix C

## Variable Basics
The default format to display numbers in Matlab is short floating point:
```matlab
>> pi
ans =
    3.1416
```
We can easily change the display format:
```matlab
>> format long
>> pi
ans =
   3.141592653589793
```
We can use j or i to define complex numbers,
```matlab
z = 2 + 3 * j
```
but either of those variables can be overwritten if not careful - Matlab allows that. Another option would be to use the "truly reserved" 1j for the imaginary number - it's not possible to overwrite.
```matlab
z = 2 + 3 * 1j
```
So, there are certain reserved variable names in Matlab (like i, j), that one should be aware of as they can be accidentally overwritten, potentially leading to unexpected behavior.
```matlab
ans          % Default variable name returned by a function with no specified output argument
pi           % π
i or j       % j
inf or Inf   % ∞
nan or NaN   % Not a number. Returned by a calculation such as 0/0 or sin(inf).
eps          % The smallest distinguishable positive double floating-point number, 2^52.
```

## Vectors and Matrices
Sequence generation:
```matlab
>> x = 1:5
x =
     1     2     3     4     5
```
We can also add a third (actually a second) argument for step, it can be float or int:
```matlab
>> x = 1:0.5:5
x =
    1.0000    1.5000    2.0000    2.5000    3.0000    3.5000    4.0000    4.5000    5.0000
```
