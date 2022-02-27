# RISC-V Vectorized Bencmark Suite

## Overview

The RISC-V Vectorized Benchmark Suite is a collection composed of seven data-parallel applications from different domains. The suite focuses on benchmarking vector microarchitectures; nevertheless, it can be used as well for Multimedia SIMD microarchitectures. Current implementation is targeting RISC-V Architectures; however, it can be easily ported to any Vector/SIMD ISA thanks to a wrapper library which we developed to map vector intrinsics and math functions to the target architecture.

The benchmark suite with all its applications and input sets is available as open source free of charge. Some of the benchmark programs have their own licensing terms which might limit their use in some cases.

The implementation is based on the working draft of the proposed [RISC-V V vector extension v1.0 Spec](https://github.com/riscv/riscv-v-spec) and [intrinsic API](https://github.com/riscv/rvv-intrinsic-doc).

If you use this software or a modified version of it for your research, please cite the paper:
Cristóbal Ramirez, César Hernandez, Oscar Palomar, Osman Unsal, Marco Ramírez, and Adrián Cristal. 2020. A RISC-V Simulator and Benchmark Suite for Designing and Evaluating Vector Architectures. ACM Trans. Archit. Code Optim. 17, 4, Article 38 (October 2020), 29 pages. https://doi.org/10.1145/3422667

## Building Vectorized Applications 

The RISC-V Vectorized Bencmark Suite has been successfully tested on [Spike RISC-V ISA Simulator](https://github.com/riscv/riscv-isa-sim)

### Setting up the environment

Recent version of LLVM (after [7f0f4ca](https://github.com/llvm/llvm-project/commit/e6de53b4de4aecca4ac892500a0907805896ed27)) is required to compile RVV 1.0 code. 

Example compilation process:

```shell
git clone https://github.com/llvm/llvm-project/
cd llvm-project

cmake -S llvm -B build -G Ninja \
    -DCMAKE_BUILD_TYPE=Release \
    -DLLVM_ENABLE_PROJECTS='clang' \
    -DLLVM_PARALLEL_LINK_JOBS=6 \
    -DLLVM_INCLUDE_{BENCHMARKS,TESTS,EXAMPLES}=OFF

ninja -C build
```

If compilation succeeded, you can find `clang` and `clang++` on `build/bin`.

GCC toolchain for target `riscv64-elf` is also required. For example it can be installed on ArchLinux by the following command:

```shell
pacman -S riscv64-elf-{gcc,newlib,binutils}
```

To simulate the compiled program, [spike](https://github.com/riscv-software-src/riscv-isa-sim) and [riscv-pk](https://github.com/riscv-software-src/riscv-pk) are required. Follow the compilation instructions on the corresponding README and install them. 

### Compile using clang for RISCV Vector Version

First, modify configurations in `Makefile.in`. You need to set your own compiler and spike/pk path. 

To compile any application you first enter in the subfolder and run the command make followed by the application name

```shell
cd _application      # change _application to the actual name
make spike_serial    # simulate non-vectorized version
make spike_vector    # simulate vectorized version
```

You can specify args other than default (given in corresponding Makefile) by passing `PROG_ARGS` to make. 

Notice for programs that output result to a file, you need to create the file before running. 

