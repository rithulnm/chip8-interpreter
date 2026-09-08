## Workflow

CMakeLists.txt describes what I want built (project name, C++ standard, which source files make up which executable) — it's a declaration, not a step-by-step procedure. When I run `cmake ..`, CMake reads that description and figures out the actual ordered build steps, writing them into a Makefile.

`make` reads that Makefile and executes the steps in order, calling g++ to do the real work. g++ compiles the source files and produces the executable — nothing more; it doesn't run it.

Running the executable (`./chip8`) is a separate, manual step I do myself. When I press F5 in VS Code, that manual step gets automated too — VS Code runs the build task first, then launches the compiled executable (through gdb, if debugging).