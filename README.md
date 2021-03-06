**DEPRECATED**: has been merged into main app repo as [branch chain](https://github.com/CMUAbstract/app-blinker/tree/chain).

An LED Blinker Application
==========================

An application that blinks two LEDs, alternating between them, implemented
using the tasks-and-channels abstraction of
[Chain](https://github.com/CMUAbstract/libchain).

Build and Run
=============

This app uses the [Maker](https://github.com/CMUAbstract/maker) build system.
Maker manages two aspects: (1) builds of dependency libraries, and (2)
co-existing builds using multiple toolchains.

Dependency libraries are managed using git submodules, in `ext` subdirectory --
this way the app can control the exact version/commit of each library, while
the library upstream is free to evolve. Dependencies are rebuilt along with the
app on purpose so that compiler flags are consistent. Dependencies are
specified in `bld/Makefile`.

Maker wraps third-party toolchains. To build this app, the TI MSP430 GCC
Toolchain (cross-compiler for MSP430) must be installed on the system. See
[documentation on
Toolchains](https://github.com/CMUAbstract/releases/blob/master/Toolchains.md).

Building with LLVM/Clang is not currently setup, but is supported by Maker.

Clone
-----

To clone this repository along with the dependency libraries:

    git clone --recursive https://github.com/CMUAbstract/app-blinker-chain


Configure
---------

Set `BOARD` environment variable, or edit it in `Makefile`, (see `Makefile.board`
in [Maker](https://github.com/CMUAbstract/maker) for a list of supported boards):

    export BOARD=mspts430

Set paths to toolchains (see `Makefile.env` in
[Maker](https://github.com/CMUAbstract/maker) for more details):

    export TOOLCHAIN_ROOT=/path/to/mspgcc
    export DEV_ROOT=/path/to/llvm/parent/dir

Configure library parameters in `bld/Makefile` as desired, e.g. MCU frequency,
console output mechanism, etc.

The app can output to a console using `libio`. Select a backend for `libio` by
setting `LIBIO_BACKEND` in `bld/Makefile`:

* `hwuart`: hardware UART (implementation in libmsp)
* `swuart`: software "bit-banged" UART (see libmspsoftuart)
* `edb`: energy-compensated output using EDB (TODO: currently broken)

The app code uses `libio` console interface, with `LOG()` and/or `PRINTF(..)`.
The `LOG` statements are enabled when building with `make VERBOSE=2 ...`.
`PRINTF` statements are enabled with `VERBOSE=1`. All output is completely
disabled with `VERBOSE=0`.

Compile
-------

See [Maker documentation](https://github.com/CMUAbstract/Maker) for detailed
guide for building with Maker. A summary is given below:

The general make target convention is `bld/<toolchain>/<target>`.  This app
supports two toolchains: `gcc` and `clang` (**TODO**: clang, not yet).

To build the app along with each dependency library:

    make bld/gcc/all

To clean the app build

    make bld/gcc/clean

To clean the app build and the build of each dependency library:

    make bld/gcc/depclean

To build each dependency library but not the app:

    make bld/gcc/dep

Flash
-----

To program the MSP430 board:

    make bld/gcc/prog

By default, the FET is assumed to be at /dev/ttyACM0, unless specified:

    make FET_DEVICE=/dev/ttyACM1 bld/gcc/prog
