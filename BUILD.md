# Build Instructions

Full build instructions will be available on [the website](https://prismlauncher.org/wiki/development/build-instructions/).

If you would like to contribute or fix an issue with the Build instructions you will be able to do so [here](https://github.com/PrismLauncher/website/blob/master/src/wiki/development/build-instructions.md).

## Getting the source

Clone the source code using git, and grab all the submodules. This is generic for all platforms you want to build on.
```
git clone --recursive https://github.com/PrismLauncher/PrismLauncher
cd PrismLauncher
```

## Linux

This guide will mostly presume commands are done by a user in the sudoers file.
### Dependencies
#### Debian
- A C++ compiler capable of building C++17 code (can be found in the package `build-essential`).
- Qt Development tools 5.12 or newer (on Debian 11 or Debian-based distributions, `qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools libqt5core5a libqt5network5 libqt5gui5`).
- `cmake` 3.15 or newer.
- `extra-cmake-modules`.
- zlib (`zlib1g-dev` on Debian 11 or Debian-based distributions).
- Java Development Kit (Java JDK) (`openjdk-17-jdk` on Debian 11 or Debian-based distributions).
- Mesa GL headers (`libgl1-mesa-dev` on Debian 11 or Debian-based distributions).
- (Optional) `scdoc` to generate man pages.

In conclusion, to check if all you need is installed (including optional):

```
sudo apt install build-essential qtbase5-dev qtchooser qt5-qmake qtbase5-dev-tools libqt5core5a libqt5network5 libqt5gui5 cmake extra-cmake-modules zlib1g-dev openjdk-17-jdk libgl1-mesa-dev scdoc
```

#### Arch
- C++ compiler: `base-devel` (Already installed in most Arch installations)
- zlib: `zlib`
- cmake: `cmake`
- Java JDK 17: `jdk17-openjdk`
- extra-cmake-modules: `extra-cmake-modules`
- Qt5: `qt5-base qt5-tools`
- Mesa GL headers: `mesa` (Already installed in most Arch installs)
- (Optional) scdoc: `scdoc`

In conclusion, to check if all you need is installed (including optional):

```
sudo pacman -S base-devel zlib cmake jdk17-openjdk extra-cmake-modules qt5-base qt5-tools mesa scdoc
```

#### Fedora
- C++ compiler: `gcc gcc-c++`
- Qt5: `qt5-qtbase-devel qtchooser`
- cmake: `cmake extra-cmake-modules`
- zlib: `zlib-devel`
- Java JDK 17: `java-17-openjdk java-17-openjdk-devel`
- Mesa GL header: `mesa-libGL-devel`
- (Optional) scdoc: `scdoc`

In conclusion, to check if all you need is installed (including optional):

```
sudo dnf install gcc gcc-c++ qt5-qtbase-devel qtchooser cmake extra-cmake-modules zlib-devel java-17-openjdk java-17-openjdk-devel mesa-libGL-devel scdoc
```

### Compiling
#### Building and installing on the system
This is usually the suggested way to build the client.

```
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX="/usr" -DENABLE_LTO=ON
cmake --build build -j$(nproc)
sudo cmake --install build
```

#### Building a portable binary

```
cmake -S . -B build -DCMAKE_INSTALL_PREFIX=install
cmake --build build -j$(nproc)
cmake --install build
cmake --install build --component portable
```

