# geogram.psm.Delaunay
geogram Delaunay pluggable software module

This is Delaunay Pluggable Software Module, extracted
from GEOGRAM source tree. It contains a standalone .cpp/.h
pair that can be used in any program and that does not have
any dependency. 

To compile the example program under Linux:
```
$ g++ -O3 -fopenmp -frounding-math -ffp-contract=off --std=c++11 Delaunay_example.cpp Delaunay_psm.cpp -o Delaunay_example -ldl -lm
```

Documentation: 
- [2d triangulations](https://github.com/BrunoLevy/geogram/wiki/Delaunay2D)
- [3d triangulations](https://github.com/BrunoLevy/geogram/wiki/Delaunay3D)

