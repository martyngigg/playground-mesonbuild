# Example f2py build with meson

## Setup environment

The example uses a Conda environment. Create and activate an environment for the desired platform:

```sh
conda env create -f ./environment-[macos,win].yml
conda activate playground-mesonbuild-dev
```

## Build with meson

Configure the project with a build directory `builddir`:

```sh
meson setup builddir
```

and compile:

```sh
meson compile -C builddir
```
