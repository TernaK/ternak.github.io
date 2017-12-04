## Caffe Installation
### macOS (Sierra 10.12.6)
Clone caffe into the home folder then create a `CAFFEROOT` environment variable by running the following command or placing this into your `.bashrc` or `.zshrc` or whatever script is run when your terminal launches;

```
export CAFFEROOT=$HOME/caffe # caffe is in the home directory, $HOME`.
```

#### `vecLib` (this is no longer necessary)
After running `cmake .. <args>`, edit `CMakeCache.txt` by finding the line pointing cmake to `vecLib` that begins with `vecLib_INCLUDE_DIR` and modify it as follows;

```
vecLib_INCLUDE_DIR:PATH=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX.sdk/System/Library/Frameworks/Accelerate.framework/Versions/Current/Frameworks/vecLib.framework/Headers
```

#### python3 - The Winning Formula for macOS 💉
- Forget anaconda. Use brew to install python3. I used 3.6.3, the default at the time.
- Install all the dependencies listed in `caffe/python/requirements.txt`.
- Install `boost-python` with brew.
- Edit the `CMakeLists.txt` and set `python_version` to `3`. Run `cmake`.
- Edit `CMakeCache.txt` and set `Boost_PYTHON-PY363_LIBRARY_RELEASE`;

```
Boost_PYTHON-PY363_LIBRARY_RELEASE=/usr/local/Cellar/boost-python/1.65.1/lib/libboost_python3.dylib`
```

Also use the following if necessary;

```
PYTHON_LIBRARY=/usr/local/Cellar/python3/3.6.3/Frameworks/Python.framework/Versions/3.6/lib/libpython3.6m.dylib 
PYTHON_INCLUDE_DIR=/usr/local/Cellar/python3/3.6.3/Frameworks/Python.framework/Versions/3.6/include/python3.6m
```
- Set the environment variable `PYTHONPATH` to `$CAFFEROOT/python` or run python from within that folder. 
