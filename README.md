# straw: Extract data quickly from Juicebox via straw
Straw is a fast C++ implementation of reading/dump for .hic files.
 
It works by reading the .hic file, finding the appropriate matrix and slice
of data, and printing the text in sparse upper triangular format.

It is not as fully featured as the Juicebox command line tools Java version;
in particular, it doesn't store the pointer data for all the matrices, only
the one queried. It also doesn't currently support reading from a URL rather
than a local file. Future versions may look more like the Java implementation. 
Currently only supporting matrices (not vectors).

Please see the below sections on compiling for C++, Python, and R.

For questions, please use
[the Google Group](https://groups.google.com/forum/#!forum/3d-genomics).

If you use this tool in your work, please cite 

**Neva C. Durand, James T. Robinson, Muhammad S. Shamim, Ido Machol, Jill P. Mesirov, Eric S. Lander, and Erez Lieberman Aiden. "Juicebox provides a visualization system for Hi-C contact maps with unlimited zoom." Cell Systems 3(1), 2016.**

## C++
Straw must be compiled with the -lz flag to include the zlib.h library:
`g++ -lz -o straw straw.cpp`

Usage: `straw <NONE/VC/VC_SQRT/KR> <hicFile> <chr1>[:x1:x2] <chr2>[:y1:y2] <BP/FRAG> <binsize> `

## R
Straw is compatible with R via the Rcpp library.  Usage is very similar to the above.  Future versions might use a different signature to call the function.

```
library(Rcpp)
sourceCpp("straw-R.cpp")
straw("NONE drosophila.hic arm_2L arm_2L BP 100000")
```

## Python 
Straw can be called from Python by using Boost <http://www.boost.org/>

The files [Jamroot](Jamroot), [straw.py](straw.py), and 
[straw-python.cpp](straw-python.cpp) are used to hook the C++ to Python. 
[straw-python.cpp](straw-python.cpp) is essentially the same as 
[straw.cpp](straw.cpp)

1. Get Boost:  
  http://www.boost.org/doc/libs/1_61_0/more/getting_started/unix-variants.html#get-boost
2. Compile bjam:  
  http://www.boost.org/doc/libs/1_49_0/more/getting_started/unix-variants.html#prepare-to-use-a-boost-library-binary
(just do --with-libraries python)
3. Type "bjam" in the directory with the files (assuming you've put boost and bjam in your path).