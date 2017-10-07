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
