+++
title = 'Embeddable Software'
date = 2024-02-03T00:22:23-08:00
+++

This aims to be a list of "embeddable" software components (typically for C/C++/Rust native code).

These are (typically statically-linked) libraries you can include inside your compiled binaries that add functionality which would usually require much larger, more complex infrastructure. Most of the time you probably do not need anything more. Probably 99% of use cases which reach for postgres can be done with sqlite just fine. Worry about scale when you have users.

## Databases

- [RocksDB](https://rocksdb.org/)
- [sqlite3](https://sqlite.org/index.html)
- [LMDB](https://www.symas.com/lmdb)
- [LevelDB](https://github.com/google/leveldb/)

## Scripting languages

- [Lua](https://lua.org/) — the 🐐 of embeddable scripting langs, which only adds 290K (of portable C99) to your binary to embed a fully-fledged interpreter
- [LuaJIT](http://luajit.org/)
- [Guile](https://www.gnu.org/software/guile/manual/guile.html#Linking-Programs-With-Guile) Scheme
- [Chibi Scheme](https://github.com/ashinn/chibi-scheme)
- [Embeddable Common Lisp](https://gitlab.com/embeddable-common-lisp/ecl)
- [mruby](https://github.com/mruby/mruby) (embeddable Ruby)
- [CHICKEN Scheme](https://call-cc.org/)

### Designed for C++ iterop

- [Clasp](https://github.com/drmeister/clasp) (Common Lisp implementation)
- [pybind11](https://pybind11.readthedocs.io/en/stable/index.html) (see also: [Embedding Python](https://docs.python.org/3/extending/embedding.html))
- [ChaiScript](https://chaiscript.com/)
