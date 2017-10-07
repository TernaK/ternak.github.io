## `Caffe` Installation Troubles

A number of issues come up when building `caffe` from source. I set up my `caffe` installation to use both the `C++` and `python` libraries on an `NVIDIA Jetson TX2` to take advantage of it's GPU for vision recognition tasks with convolutional neural nets. After following the basic installation instuctions for dependencies on the `caffe` homepage, the compilation stage may not go according to plan. The following are common problems and how to resolve them;

#### Failing to find `opencv`

  This might happen if `opencv` was installed from source. With `pkg-config` the `caffe` `Makefile.config` can find that by uncommenting `# USE_PKG_CONFIG := 1`. Or just use `cmake` to build.
#### Failing to link to the correct `hdf5` libraries

  If `hdf5` was installed, it's likely actually installed as `hdf5_serial`. Add the path to the `hdf5` header files to `INCLUDE_DIRS` in `Makefile.config`. The second part of the solution involves creating symbolic links `hdf5.so` to `hdf5_serial.so` inside the `hdf5` libraries folder. Do this on the terminal with `ln -s hdf5_serial.so hdf5.so` form within the `hdf5` libraries folder. `sudo` might be required.
  
#### Failing to build tests on `TX2`

  This is because the right CUDA compute capability (`6.2`, as at the time of writing this with a `TX2` recently flashed with Jetson Jetpack 3.1) is missing. Building with `cmake` will automatically resolve this, however you can also add `-gencode arch=compute_62,code=compute_62` to `CUDA_ARCH` in  `Makefile.config`.

Just use `cmake` to save you a lot of pain and anguish.
