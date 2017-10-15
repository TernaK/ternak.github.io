### Lazily specify header and library search paths, and libraries to link using `pkg-config`
Here's a simple `opencv` program;
```c++
# program.cpp
#include <iostream>
#include <opencv2/opencv>
using namespace cv;

int main() {
  Mat matrix = Mat::zeros(5, 5, CV_8U);
  cv::resize(matrix, matrix, Size(3,3));
  std::cout << matrix << std::endl;
}
```

To compile;

`g++ -std=c++11 program.cpp -o program -I/usr/local/include -L/usr/local/libraries -lopencv_core -lopencv_imgproc`

A shorthand way of doing this is;

`g++ -std=c++11 program.cpp -o program $(shell pkg-config --libs --cflags opencv)`

Use this if you're especially too lazy to write the path names or the list of required libraries.

### Using `pkg-config` to set libraries and compilation options
_References_
- [FindPkgConfig](https://cmake.org/cmake/help/v3.0/module/FindPkgConfig.html)
- [googletest](https://github.com/google/googletest/blob/master/googletest/docs/Pkgconfig.md)

This is how to find the required librairies and include directories for a target. This example creates a unit test target that uses the  `googletest` framework.

```
find_package(PkgConfig)
pkg_search_module(GTEST REQUIRED gtest_main)

add_executable(testapp samples/sample3_unittest.cc)
target_link_libraries(testapp ${GTEST_LDFLAGS})
target_compile_options(testapp PUBLIC ${GTEST_CFLAGS})

include(CTest)
add_test(first_and_only_test testapp)

### Using pkg_search_module(XPREFIX ...) defines the following variables
# <XPREFIX>_FOUND          ... set to 1 if module(s) exist
# <XPREFIX>_LIBRARIES      ... only the libraries (w/o the '-l')
# <XPREFIX>_LIBRARY_DIRS   ... the paths of the libraries (w/o the '-L')
# <XPREFIX>_LDFLAGS        ... all required linker flags
# <XPREFIX>_LDFLAGS_OTHER  ... all other linker flags
# <XPREFIX>_INCLUDE_DIRS   ... the '-I' preprocessor flags (w/o the '-I')
# <XPREFIX>_CFLAGS         ... all required cflags
# <XPREFIX>_CFLAGS_OTHER   ... the other compiler flags
```
