# boost-python-cmake-mac
Yep, use boost python under CMake on a Mac.

Drawn from [Feral Chicken's]((https://feralchicken.wordpress.com/2013/12/07/boost-python-hello-world-example-using-cmake/) post and updated after numerous hours on StackOverflow.

### Build & Run

Go into the build dir and run

```
make ..
make
```

Then you can open a Python shell in the same dir and do

```
>>> import greet_ext
>>> greet_ext.greet()
'Hello world'
```

## Notes

The real trick seemed to have CMake produce a `.so` file instead of a `.dylib` file with the lines in CMake

```
if(APPLE)
set(CMAKE_SHARED_LIBRARY_SUFFIX ".so")
endif(APPLE)
```

Also, at a certain point I was getting an error that turned out to be that CMake's `find_package( PythonLibs 2.7 REQUIRED )` command found the System Python under `/System/Library/Frameworks/Python.framework/Versions/2.7/include/python2.7`.  This was linked to the binary `/usr/bin/python` which was version 2.7.10.  But when I used the command `python` I got `/usr/local/bin/python` which was installed by Homebrew and version 2.7.12.

