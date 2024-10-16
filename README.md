# Valgrind Exercise

## Problems fixed in shell-app
- Memory leak at AnalogSensor.cpp:16. In the function, memory is allocated during runtime on the heap using the new, but the memory was not deleted later
    - Fix: Use the delete function.
- uninitialized variable in main.cpp:5. terminator was declared as bool but was never initialized.
    - Fix: Initialise the variable before use

## What happens when the executable is linked statically?  Does Valgrind still detect those same bugs?
When the executable is linked statically, Valgrind can still find bugs that were not the same but pointed in a similar direction. <br>
By default, no replacement is done for a statically linked binary or alternative libraries, allocation functions are intercepted by default in any shared library or the executable if they are exported as global symbols.

## Why and Why not?
For statically linked apps valgrind can only intercept allocation functions by default. However, shared valgrind can intercept many more functions not just allocation functions.

```bash

#Command used to run Valgrind
valgrind --track-origins=yes --leak-check=full --leak-resolution=high "path to executable"

Details of files added

valgrind_output_errorsFixed_with_staticLinked.txt
#contains the output of valgrind when the app is not statically linked and produces the above two errors

Valgrind_Output_error_FIxed.txt
#contains the output of valgrind when the app is not statically linked and produces no errors

valgrind_output.txt
#contains the output of Valgrind when the app is statically linked

```


## Standard install via command-line
```bash
# Configure the project and generate a native build system:
  # Must re-run this command whenever any CMakeLists.txt file has been changed.
  cmake -S ./ -B build/
# To build with debugging information, do:
  cmake -S ./ -B build/ -D CMAKE_BUILD_TYPE=Debug
# Compile and build the project:
  # rebuild only files that are modified since the last build
  cmake --build build/
  # or rebuild everything from scratch
  cmake --build build/ --clean-first
  # to see verbose output, do:
  cmake --build build/ --verbose
# Run program:
  ./build/app/shell-app
# Clean
  cmake --build build/ --target clean
# Clean and start over:
  rm -rf build/
```
