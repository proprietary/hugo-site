+++
title = 'Compiling Emacs on Mac'
date = 2024-01-31T07:05:56-08:00
draft = false
+++

This is how to build Emacs from source on macOS (working as of macOS Sonoma 14.2) (sorry Stallman). We want all the latest bells and whistles:

- native compilation of Elisp
- tree-sitter
- libjannson for fast JSON parsing (useful for LSP modes)

Compiling the latest Emacs from HEAD also gives you access to the latest features, like Eglot (language server built-in to Emacs). You also may wish to compile with debug information if you want to hack on Emacs itself.

## Install dependencies

```bash
brew install \
	pkg-config \
	texinfo \
	libgccjit \
	autoconf \
	automake \
    make \
	jansson \
	gnutls \
	mailutils \
	imagemagick \
	tree-sitter \
	mailutils
```

or using MacPorts:

```bash
sudo port install \
	pkg-config \
	gcc13 \
	libgcc13 \
	texinfo \
	autoconf \
	automake \
	jansson \
	gnutls \
	ImageMagick \
	tree-sitter

# Set location of libgccjit in CFLAGS (used later in build)
CFLAGS="-O3 \
	-march=native \
	-I/opt/local/include/gcc13 \
	-L/opt/local/lib/gcc13 \
	-Wl,-rpath,/opt/local/lib/gcc13 "
```

Make sure `pkg-config` can find the libraries you just installed:

```bash
export PKG_CONFIG_PATH="$PKG_CONFIG_PATH:/usr/local/lib/pkgconfig:/opt/local/lib/pkgconfig"
```

## Build instructions

Clone source code and build:

```bash
git clone git://git.savannah.gnu.org/emacs.git
cd emacs
./autogen.sh

# Change "--prefix=..." as you wish
./configure \
    --prefix=/usr/local \
    --with-ns \
    --disable-ns-self-contained \
    --with-json \
    --with-tree-sitter \
    --with-native-compilation \
    --with-imagemagick \
    --with-mailutils \
    --without-compress-install \
    CFLAGS="${CFLAGS}"
gmake -j $(sysctl -n hw.ncpu)
sudo gmake install
```

You may need to change some of the paths (like `/opt/local/lib`, `/opt/local/include`) if you have a non-standard directory for MacPorts or Homebrew. If you are having trouble, make sure that these paths point to where `$ find / -name 'libgccjit*'` .dylib's show up.

After the build is successful, you can find the `Emacs.app` in `./nextstep`. You may want to copy this to `/Applications` like a normal Mac App:

```bash
cp -r ./nextstep/Emacs.app /Applications
```

Note that when you use the configure flag `--disable-ns-self-contained` as above, you also install Lisp files to the system `--prefix` directory, so you are able to use Emacs in the terminal as well without issues, but only if you use that flag.

Happy Emacsing!

## See also

[How to Get Started with Tree-Sitter](https://www.masteringemacs.org/article/how-to-get-started-tree-sitter)

[Speed up Emacs with libjansson and native elisp compilation](https://www.masteringemacs.org/article/speed-up-emacs-libjansson-native-elisp-compilation)
