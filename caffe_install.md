## Caffe Installation
### macOS (Sierra 10.12.6)
1. Clone caffe into the home folder (strongly recommended).
2. Make a `build` directory and from there, execute;

    `cmake .. <args> # args should set caffe to build for CPU mode`
    
    `vecLib` might have to be found as part of the `Accelerate` framework (see the `vecLib` section below). Resolve all dependencies then `make` and `sudo make install`. If everything is fine, the build outputs will be inside `caffe/build/install` including `lib`, `include` for the library and include files respectively. 
3. Create a `CAFFEROOT` environment variable by running the following command or placing this into your `.bashrc` or `.zshrc` or whatever script is run when your terminal launches;

    `export CAFFEROOT=$HOME/caffe # caffe is in the home directory, $HOME`.

#### `vecLib`
After running `cmake .. <args>`, edit `CMakeCache.txt` by finding the line pointing cmake to `vecLib` that begins with `vecLib_INCLUDE_DIR` and modify it as follows;

`vecLib_INCLUDE_DIR:PATH=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/System/Library/Frameworks/Accelerate.framework/Versions/Current/Frameworks/vecLib.framework/Headers`

#### python3 Anaconda build
```
cmake .. -DPYTHON_LIBRARY=$HOME/anaconda3/lib/libpython3.6m.dylib -DPYTHON_EXECUTABLE=$HOME/anaconda3/bin/python \
         -DPYTHON_INCLUDE_DIR=$HOME/anaconda3/include/python3.6m \
         -DNUMPY_INCLUDE_DIR=$HOME/anaconda3/lib/python3.6/site-packages/numpy/core/include
```
