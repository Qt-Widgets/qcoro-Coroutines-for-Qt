# Building and Using QCoro

## Building QCoro

QCoro uses CMake build system. You can pass following options to the `cmake` command when building
QCoro to customize the build:

* `-DQCORO_BUILD_EXAMPLES` - whether to build examples or not (`ON` by default).
* `-DQCORO_ENABLE_ASAN` - whether to build QCoro with AddressSanitizer (`OFF` by default).
* `-DBUILD_SHARED_LIBS` - whether to build QCoro as a shared library (`OFF` by default).
* `-DBUILD_TESTING` - whether to build tests (`ON` by default).
* `-DUSE_QT_VERSION` - set to `5` or `6` to force a particular version of Qt. When not set the highest available version is used.
* `-DQCORO_WITH_QTDBUS` - whether to compile support for QtDBus (`ON` by default).
* `-DQCORO_WITH_QTNETWORK` - whether to compile support for QtNetwork (`ON` by default).

```
mkdir build
cd build
cmake .. <CMAKE FLAGS>
make
# This will install QCoro into /usr/local/ prefix, change it by passing -DCMAKE_INSTALL_PREFIX=/usr
# to the cmake command above.
sudo make install
```

## Add it to your CMake

Depending on whether you want to use Qt5 or Qt6 build of QCoro, you should use `QCoro5` or QCoro6` in your
CMake code, respectively. The example below is assuming Qt6:

```cmake
# Use QCoro5 if you are building for Qt5!
find_package(QCoro6 REQUIRED COMPONENTS Core Network DBus)

# Set necessary compiler flags to enable coroutine support
qcoro_enable_coroutines()

...

target_link_libraries(your-target QCoro::Core QCoro::Network QCoro::DBus)
```

Note the missing Qt version number in the `QCoro` target namespace: QCoro provides both
versioned (`QCoro5` and `QCoro6`) namespaces as well as version-less namespace, which is
especially useful for transitioning codebase from Qt5 to Qt6.


