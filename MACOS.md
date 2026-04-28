# Building LibreDWG on macOS

To compile LibreDWG on macOS, follow these steps:

## 1. Install Dependencies

Using [Homebrew](https://brew.sh/):

```sh
brew install autoconf automake libtool pkg-config pcre2
```

Optional dependencies for bindings:
```sh
brew install swig python
```

## 2. Build using Autotools (Recommended)

```sh
sh autogen.sh
./configure
make
make check
```

If `configure` fails to find `pcre2` or `libiconv`, you may need to set environment variables:

```sh
export LDFLAGS="-L/opt/homebrew/lib"
export CPPFLAGS="-I/opt/homebrew/include"
export PKG_CONFIG_PATH="/opt/homebrew/lib/pkgconfig"
./configure
```

## 3. Build using CMake

```sh
cmake -B build
cmake --build build
```

## Common Issues

### iconv errors
macOS comes with a version of `libiconv` in `/usr/lib`, but sometimes the build system might prefer the Homebrew version. If you see iconv-related errors, try:
```sh
brew install libiconv
export LDFLAGS="-L/opt/homebrew/opt/libiconv/lib $LDFLAGS"
export CPPFLAGS="-I/opt/homebrew/opt/libiconv/include $CPPFLAGS"
```

### Python bindings
macOS system Python often lacks necessary modules. It is recommended to use the Homebrew Python and set the `PYTHON` environment variable:
```sh
export PYTHON=$(which python3)
./configure
```
