# PyTorch ATen minimal build from prebuilt libraries
This CMakeLists.txt manages the building of a simple C++ program based on the ATen tensor library and libtorch built from [PyTorch 1.6](https://github.com/pytorch/pytorch/tree/1.6)
## Simple C++ program : `aten_min.cpp` adapted from [PYTORCH C++ API](https://pytorch.org/cppdocs/)
    #include <ATen/ATen.h>

    int main() {
      at::Tensor a = at::ones({2, 2}, at::kInt);
      at::Tensor b = at::randn({2, 2});
      auto c = a + b.to(at::kInt);
    }
## Prerequisites
1. Clone [PyTorch 1.6](https://github.com/pytorch/pytorch/tree/1.6) and adjust the [CMakeLists.txt](CMakeLists.txt) variable `PYTORCH_SRC_DIR` to point to the local repository, for example `set(PYTORCH_SRC_DIR ../pytorch)`
2. Install the [PyTorch prerequisites](https://github.com/pytorch/pytorch/tree/1.6#from-source)
3. Build libtorch, see [build_libtorch](https://github.com/shanemcandrewai/build_libtorch) for an example
4. Adjust [CMakeLists.txt](CMakeLists.txt) variables `PYTORCH_SRC_DIR`, `LIBTORCH_SRC_DIR` and `LIBTORCH_LIB_DIR` to point to the local repositories.
## Usage
### Generate the project buildsystem
    cmake -S . -B build
#### Cmake options
##### CMAKE_BUILD_TYPE 
The default buid type is `Release`. For a debug build pass option `-D CMAKE_BUILD_TYPE=Debug`
##### CMAKE_CXX_FLAGS
###### GCC
`-Og` enables optimizations that do not interfere with debugging
#### Example
    cmake -DCMAKE_CXX_FLAGS=-Og -DCMAKE_BUILD_TYPE=Debug -S . -B build
### Build the project
    cmake --build build
### Execute
    ./build/aten_libtorch
### Cleaning / trouble-shooting
#### Linux
    rm build/CMakeCache.txt
    rm -rf build
    diff --color=always -u file1 file2 | less -r
#### Windows
    del build/CMakeCache.txt
    rmdir /s /q build
    mklink /d build d:\build
#### Clean PyTorch source without using standard ignore rules
    git clean -dfx
