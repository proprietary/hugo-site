+++
title = 'Building latest Clang+LLVM on MacOS'
date = 2023-12-10T21:35:52-08:00
draft = false
+++

First, ensure you have the latest Apple Clang installed.

```bash
xcode-select --install
```

Then this will build all LLVM projects (e.g., `clang`, `lldb`, `libc++`, `openmp` ...), working as of macOS 14 (Sonoma).

```bash
git clone --depth=1 https://github.com/llvm/llvm-project
LLVM_SOURCE_DIR="$(pwd)/llvm-project"
cd /tmp
mkdir llvm-build && cd llvm-build
MY_LLVM_INSTALL_PATH=$HOME/.local # or something else; change this
mkdir -p $MY_LLVM_INSTALL_PATH
cmake -S "$LLVM_SOURCE_DIR/llvm" \
  -DCMAKE_BUILD_TYPE=Release \
  -DDEFAULT_SYSROOT=$(xcrun --show-sdk-path) \
  -DLLVM_ENABLE_PROJECTS="all" \
  -DLLVM_ ENABLE_RUNTIMES="all" \
  -DCMAKE_INSTALL_PREFIX=$HOME/.local
make -j$(sysctl -n hw.ncpu)
make install
```

The key is to not have any existing LLVM artifacts on your `$PATH` or `$LD_LIBRARY_PATH` **except** for those of the standard Apple Clang.