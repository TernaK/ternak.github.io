## Building opencv

### Basic build
```
cmake .. -DBUILD_TESTS=OFF -DBUILD_PERF_TESTS=OFF
```

### For python3 (Anaconda)
The following assumes Anaconda has been installed to the home directory in `$HOME/anaconda3`.

```
cmake .. -DBUILD_opencv_python3=ON -DBUILD_opencv_python2=OFF \
  -DPYTHON_LIBRARIES=$HOME/anaconda3/lib/libpython3.6m.dylib \
  -DPYTHON3_PACKAGES_PATH=$HOME/anaconda3/lib/python3.6/site-packages \
  -DPYTHON3_INCLUDE_DIR=$HOME/anaconda3/include/python3.6m \
  -DPYTHON3_EXECUTABLE=$HOME/anaconda3/bin/python \
  -DPYTHON3_NUMPY_INCLUDE_DIRS=$HOME/anaconda3/lib/python3.6/site-packages/numpy/core/include
```
