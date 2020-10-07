# PyTorch libtorch build example 

This CMakeLists.txt manages the building of a minimal libtorch from [PyTorch 1.6](https://github.com/pytorch/pytorch/tree/1.6)

## Prerequisites

1. Clone [PyTorch 1.6](https://github.com/pytorch/pytorch/tree/1.6) and adjust the [CMakeLists.txt](CMakeLists.txt) variable `PYTORCH_SRC_DIR` to point to the local repository, for example `set(PYTORCH_SRC_DIR ../pytorch)`

2. Install the [PyTorch prerequisites](https://github.com/pytorch/pytorch/tree/1.6#from-source)

## Usage
### build the library
#### Linux
    rm -rf build && cmake -S . -B build
#### Windows
    rmdir /s /q build && cmake -S . -B build
#### Cmake options
##### RESET
This restores the PyTorch source working tree from HEAD and cleans recursively without respecting `.gitignore` This can be enabled by passing the option `-D RESET=1`.
##### BUILD_SHARED_LIBS
The build generates a shared library by default. This can be disabled by passing the option `-D BUILD_SHARED_LIBS=0`.
##### DEBUG
The build has debugging information by default. This can be disabled by passing the option `-D DEBUG=0`.
## Result
`[build derectory]/lib` contains the libraries and `[build directory]/build/aten/src/` contains the generated header file `TensorBody.h`
