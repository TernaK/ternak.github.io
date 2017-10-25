### macOS (Sierra 10.12.6)
1. Clone <http://github.com/weiliu89/caffe> into the home folder (strongly recommended).
2. Checkout the `ssd` branch.
3. Make a `build` directory and from there, execute `cmake .. -DCPU_ONLY=ON`. `vecLib` might have to be found as part of the `Accelerate` framework (see the `vecLib` section below). Resolve all dependencies then `make` and `sudo make install`. If everything is fine, the build outputs will be inside `caffe/build/install` including `lib`, `include` for the library and include files respectively. 
4. Create a `CAFFEROOT` environment variable by running the following command or placing this into your `.bashrc` or `.zshrc` or whatever script is run when your terminal launches;

    `export CAFFEROOT=$HOME/caffe/build/install # assuming caffe is in the home directory $HOME`.

    The last step is crucial for `planck_detector` to be able to build as its cmake must find your caffe installation.
5. CMakeLists.txt can find caffe through;
    ```
    include_directories($ENV{CAFFEROOT}/include)
    link_directories($ENV{CAFFEROOT}/lib)
    ```

#### `vecLib`
After running `cmake .. -DCPU_ONLY=ON`, edit `CMakeCache.txt` by finding the line pointing cmake to `vecLib` that begins with `vecLib_INCLUDE_DIR` and modify it as follows;

`vecLib_INCLUDE_DIR:PATH=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/System/Library/Frameworks/Accelerate.framework/Versions/Current/Frameworks/vecLib.framework/Headers`
