# C++ Library for Gaussian Quadrature with Singular weights

### Dependencies
GQJacobi is a library that relies on Eigen, which you can download by running;
```
brew install eigen
```
If you are building with CMake, this isn't a problem. However, if you are simply including into your `include` directory, you will have to set your compiler path to wherever you have installed Eigen.

You will also need to have `Boost` installed, which you can do by typing:
```
brew install boost
```


## Installation


To use this header-ony library, clone this repo and run the following commands in the directory you're cloned to:
### Setup with CMake
```
$ cd singular-gauss-quad
$ mkdir build
$ cd build
$ cmake ..
$ sudo cmake --build . --target install
```
If you get the message `Could NOT find Boost (missing: Boost_DIR)` or `Could NOT find Eigen3 (missing: Eigen3_DIR)` when installing, then go back to the previous step and install the dependencies.
The `sudo` is very important, as files will be crated & require admin privileges.

### Setup by including

As this is a header-only library, you can also dowload ``gauss-jacobi.hpp`` and put it into your 'include' file, for exmaple. However, it is important to note the following:



## Building

### With CMake
Your root CMake will need to include the following lines

```
find_package(GQJacobi)
target_link_libraries(yourprojectname PUBLIC GQJacobi::GQJacobi)
```

for `GQJacobi` to work. The rest is already handled (dependencies and such).

### As an include
You will need to configure your project in such a way that the `gauss-jacobi.hpp` file can properly include `Eigen`.


**NOTE!** _You may need to add the include path to Eigen in your environment! The code compiles and runs, but the IDE or editor may fuss about, thus making the experience uncomfortable._

## Usage

Once `GQJacobi` is installed and incuded, import is by typing:
```
#include "GQJacobi/gauss-jacobi.hpp"
```

### Example
````
template <typename T>
double square(T x)
{
    return x*x;
}

GQJacobi::GaussJacobiRule<double> gqj(4, -0.8, -0,2); // generates a 4-point Gauss-Jacobi quadrature rule

//computation
double quad = gqj(square<double>);

// now quad contains the integral from -1 to 1 of x^2
``` 