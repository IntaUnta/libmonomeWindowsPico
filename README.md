This fork makes a few changes to `src/platform/windows.c` to fix detection of the neotrellis monome using an RP2040 on Windows.

## Serialosc build instructions using this fork

**Requirements:**
- [MSYS2](https://www.msys2.org/)

**Install required packages in msys2 MinGW 64-bit terminal:**
```bash
pacman -S mingw-w64-x86_64-cmake mingw-w64-x86_64-gcc mingw-w64-x86_64-ninja git
```

**Clone serialosc:**
```bash
git clone https://github.com/monome/serialosc
cd serialosc
```

**Initialize submodules:**
```bash
git submodule update --init --recursive
```

**Replace libmonome with this fork:**
```bash
cd third-party/libmonome
git remote add pico https://github.com/IntaUnta/libmonomeWindowsPico
git fetch pico
git checkout pico/main
cd ../..
```

**Build:**
```bash
mkdir build
cd build
cmake .. -DCMAKE_BUILD_TYPE=Release -G Ninja
ninja
```

**Test:**
```bash
./bin/serialoscd.exe
```

You should see:
> serialosc [mXXXXXXX]: connected, server running on port XXXXX


libmonome:

    libmonome is a library for easy interaction with monome devices. It
    currently runs on Linux (on which it is primarily developed), OpenBSD, and
    Darwin/OS X.

    It was developed to make monome devices easy to use with programming
    languages like C and Python, and adding wrappers for use in your favorite
    language with a suitable FFI is straightforward.

    libmonome has support for 40h and series devices through a unified API,
    and by default includes a third backend which wraps around the OSC
    protocol and presents the same API as a physical device. This means that a
    program written using libmonome can, at runtime, decide whether to
    communicate with a running monomeserial instance over OSC or whether to
    access the physical device directly.

    build like:

        $ mkdir build; cd build
        $ cmake ..
        $ make; sudo make install

    libmonome was written by william light (visinin on the monome forums).
    You can contact him at <wrl@illest.net>.