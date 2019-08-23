## `cmake + pkg-config` and `makefile` tips
### `cmake` template
```cmake
cmake_minimum_required(VERION 3.0)
project(<project_name>)
set(CMAKE_CXX_STANDARD 11)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/bin)
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/lib)

set(libraries <libraries>)
set(include_dirs <include directories>)

set(library_srcs <source files>)
add_library(<library_name> ${executable_srcs})
target_link_libraries(<library_name> PUBLIC ${libraries})
target_include_directories(<library_name> PUBLIC ${include_dirs})

set(executable_srcs <source files>)
add_executable(<executable_name> ${executable_srcs})
target_link_libraries(<executable_name> ${libraries})
target_include_directories(<executable_name> PRIVATE ${include_dirs})
```

### Lazily specify header and library search paths and libraries to link using `pkg-config`
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

```g++ -std=c++11 program.cpp -o program -I/usr/local/include -L/usr/local/libraries -lopencv_core -lopencv_imgproc```

A shorthand way of doing this is;

```g++ -std=c++11 program.cpp -o program `pkg-config --libs --cflags opencv` ```
