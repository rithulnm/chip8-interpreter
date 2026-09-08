## Folder Structure

    chip8-interpreter/
        build/
        docs/
        roms/
        src/
        CMakeLists.txt

## 1. Install CMake

```bash
sudo apt update
sudo apt install cmake
```

## 2. Install build tools

```bash
sudo apt install build-essential   # installs g++ (compiler) and make
sudo apt install gdb               # debugger
```

## 3. CMakeLists.txt

```cmake
cmake_minimum_required(VERSION 3.16)
project(chip8_interpreter)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

add_executable(chip8 src/main.cpp src/chip8.cpp)
```

## 4. .vscode files

**tasks.json**
```json
{
    "version": "2.0.0",
    "tasks": [
        {
            "label": "cmake build",
            "type": "shell",
            "command": "cmake",
            "args": ["--build", "${workspaceFolder}/build"],
            "options": {
                "cwd": "${workspaceFolder}/build"
            },
            "problemMatcher": ["$gcc"],
            "group": {
                "kind": "build",
                "isDefault": true
            }
        }
    ]
}
```

**launch.json**
```json
{
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Debug chip8",
            "type": "cppdbg",
            "request": "launch",
            "program": "${workspaceFolder}/build/chip8",
            "args": [],
            "stopAtEntry": false,
            "cwd": "${workspaceFolder}",
            "environment": [],
            "externalConsole": false,
            "MIMode": "gdb",
            "miDebuggerPath": "/usr/bin/gdb",
            "preLaunchTask": "cmake build"
        }
    ]
}
```

This wires F5 to build then debug directly. Alternatively, use `Ctrl+Shift+P` → `CMake: Debug` to bypass tasks.json/launch.json entirely.

## 5. VS Code's C/C++ extension can silently overwrite tasks.json

If you use "Add Debug Configuration" or let the C/C++ extension auto-generate a task, it creates its OWN tasks.json with label "C/C++: gcc build active file" — this OVERWRITES your custom "cmake build" task and breaks preLaunchTask in launch.json.

Fix: after any auto-generation, run `cat .vscode/tasks.json` and confirm the label is still "cmake build" before using F5.