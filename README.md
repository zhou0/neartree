# NearTree

## Release 5.1.1 (24 April 2016)

(c) Copyright 2001, 2008, 2009, 2010, 2011, 2014, 2016 Larry Andrews. All rights reserved.

Based on:
* Lawrence C. Andrews, Herbert J. Bernstein, "NearTree, a data structure and a software toolkit for the nearest-neighbor problem", *J. Appl. Crystallogr.*, Volume 49, Part 3 (June 2016), doi: 10.1107/S1600576716004350, ISSN:1600-5767.
* Larry Andrews, "A template for the nearest neighbor problem", *C/C++ Users Journal*, Volume 19, Issue 11 (November 2001), 40 - 49 (2001), ISSN:1075-2838, [www.ddj.com/architect/184401449](http://www.ddj.com/architect/184401449)

---

### LGPL NOTICES

This library is free software; you can redistribute it and/or modify it under the terms of the GNU Lesser General Public License as published by the Free Software Foundation; either version 2.1 of the License, or (at your option) any later version.

This library is distributed in the hope that it will be useful, but WITHOUT ANY WARRANTY; without even the implied warranty of MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE. See the GNU Lesser General Public License for more details.

---

## Introduction

This is a release of an API for finding nearest neighbors among points in spaces of arbitrary dimensions. This release provides a C++ template, `TNear.h`, and a C library, `CNearTree.c`, with example/test programs.

## Installation

### Using CMake (Recommended)

This project supports CMake (version 3.5 or higher). To build the project:

```bash
mkdir build
cd build
cmake ..
make
```

This will build the libraries and the example/test programs.

### Using Makefile

For unix or MINGW, you can use the provided `Makefile`. You will need `libtool` on your system.

To see the current settings for a build, execute:
```bash
make
```

To compile:
```bash
make clean
make all
```

To run tests:
```bash
make tests
```

To install:
```bash
make install
```

## The C++ template: TNear.h

### Synopsis

```cpp
#include <TNear.h>

// Coordinate Type (e.g., double), Distance Type (e.g., double),
// and an optional minimum distance value
CNearTree<T, DistanceType, distMinValue> neartree;
```

### Key Member Functions

*   `insert(const T& t)`: Inserts an object into the tree.
*   `NearestNeighbor(const DistanceType& dRadius, T& tClosest, const T& t)`: Finds the nearest neighbor within a given radius.
*   `FarthestNeighbor(T& tFarthest, const T& t)`: Finds the farthest neighbor.
*   `FindInSphere`, `FindOutSphere`, `FindInAnnulus`: Search for points in specific regions.
*   `FindK_NearestNeighbors`, `FindK_FarthestNeighbors`: Search for the K nearest or farthest points.
*   `size()`: Returns the total number of objects.

## The C NearTree API: CNearTree.c

The C API provides a similar set of functionality for C applications. It depends on the `CVector` library.

### Key Functions

*   `CNearTreeCreate`: Create a new neartree.
*   `CNearTreeInsert`: Insert a coordinate and an optional object.
*   `CNearTreeNearestNeighbor`: Find the nearest neighbor.
*   `CNearTreeFree`: Free the neartree.

## Random Number Generator: rhrand.h

A portable pseudo-random number generator is included in `rhrand.h`. It provides both a C++ class `RHrand` and a C interface.

---

**Updated:** 25 April 2016
**Contact:** andrewsl@ix.netcom.com
