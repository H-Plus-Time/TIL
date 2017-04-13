# Building from source

On resource-limited systems, fastcomp by default eats all the memory, so
it is best to allow the emscripten sdk to finish its clone of fastcomp,
and begin the build process, before stopping it, changing directory to
./clang/fastcomp/build_incoming_64bit and executing make with the
desired level of parallelism. i.e:
```bash
cd clang/fastcomp/build_incoming_64bit
make -j3
```

Binaryen by default builds with sse2 and fpmath=sse2 enabled. Neither of
these are compatible on ARM.

The relevant file to change is binaryen/master/CMakeLists.txt. Any
reference to sse2 must be removed.
