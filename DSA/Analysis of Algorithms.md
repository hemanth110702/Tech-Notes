# Analysis of Algorithms

## The Role of Algorithm 

Factors affecting prog. performance
1) DS & Algo
2) H/w -> desktop vs desktop
3) compiler -> 4 - 6 cycle optimization
4) OS (link system libraries)
5) prog. lang (Microsoft Visual C++ > GCC)

Items 2-5 are considered secondary factors.
none of these give 100 times better result for prog. performance

Calculations:

merge sort -> O(n log n)
insertion sort -> O(n²)

M-S [Merge Sort] speedup = O(n²) / O(n log n) = n / log n 

if n = 1000 => 1000 / log₂(1000) => 100

M-S is 100 times faster than I-S [Insertion Sort]