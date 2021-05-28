# Build and Installation Instructions with Meson

Meson is a modern and fast build system with a lot of features. You can
find its documentation at [mesonbuild.com](https://mesonbuild.com/).

## Install Dependencies

=== "Fedora"

    ```bash
    dnf install meson qt5-qtbase-devel rtaudio-devel "pkgconfig(jack)" help2man
    ```

=== "Debian/Ubuntu"

    ```bash
    apt install meson build-essential qtbase5-dev librtaudio-dev libjack-jackd2-dev help2man
    ```

=== "MacOS"

    ```bash
    brew install meson qt rt-audio jack help2man
    ```

    Meson might not find qt when installed with brew. But brew tells you to set
    PKG_CONFIG_PATH to a directory where it finds qt's pkgconfig file.
    This directory has to be set as additional pkgconfig path in meson:

    ```bash
    meson --buildtype release --pkg-config-path PATH_GIVEN_BY_BREW build_release
    ``` 

## Build

Meson builds in a separate directory. It doesn't touch anything of your project.
This way you can have seperate debug and release build directories for example. 

Prepare your build directory:
```bash
meson --buildtype release build_release
meson --buildtype debugoptimized build_debug
```

Meson automatically downloads RtAudio and compiles it
as a subproject, if RtAudio is not found on your system.
If `help2man` is found, Meson will create a manpage from `jacktrip --help`.

Now build with:
```bash
cd build_release
meson compile
```

Install with:
```bash
sudo meson install
```

## Configure

If you are in a build directory, `meson configure` shows you all available options.
Current project options are `jack`, `nogui`, `rtaudio` and `wair`.
Meson shows you also the options of subprojects like RtAudio.
