# Building from source

On resource-limited systems, fastcomp by default eats all the memory, so
one MUST specify the number of cores when installing via the emscripten
sdk, like so:
```bash
./emsdk install -jX <blah> <blah>
```

Where x is a small integer - on a system with 4GB RAM, 3 cores is
tolerable (the default is n_cores - 1 anyway).

The clang compilation works fine under constrained memory, but the
linking step (to create the clang binary) necessarily consumes an
enormous amount of memory (on the order of 6-10GB). Create a swapfile OR
(given the former at best earns a 50/50 chance of success) swap the GNU
linker for the gold linker - a symlink from wherever gold is (say,
/usr/bin/gold) to a local bin ($HOME/bin), in combination with setting
PATH to $HOME/bin:$PATH (in order to bump up the priority of your symlinked gold binary) works well.

When installing on ARM systems, emscripten identifies the architecture
correctly for all but the nodejs download - this seems to be fixed to
the x86 version of whatever ```getconf LONG_BIT``` returns (32 -> x86, 64 -> x86_64).
For the meantime, simply copy the contents of the correct tarball (of a
reasonable version - the LTS release, currently at v6, works well) to
the location of emscripten's erroneous version.

Also, specifying --shallow helps with the download time.

Binaryen previously defaulted to sse2 and fpmath=sse2 enabled. Neither of
these are compatible on ARM. The relevant file to change is binaryen/master/CMakeLists.txt. Any
reference to sse must be removed.
 
 Update: binaryen no longer exhibits that problem, thanks to the gracious maintainers.
