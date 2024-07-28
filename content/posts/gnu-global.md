+++
title = 'Using GNU Global for source code navigation'
date = 2024-07-28T13:56:55-07:00
draft = false
+++

# Using GNU Global + universal-ctags for source code navigation

Sometimes a [LSP](https://langserver.org/) is not necessary or too
much bloat. In very large codebases LSPs or IDEs can keel over. Or
sometimes there simply isn't a LSP for the language (like SQL—dealing
with a huge tree of SQL files is what led me to reach for Global in
the first place). The old TAGS style of code browsing still works.
Sometimes it's the better tool for the job.

[Universal Ctags](https://ctags.io) can parse dozens of languages out
of the box. It can generate "tags" files which are essentially
databases of references to definitions in source code. Using these
tags files, we can configure our editors to jump-to-definition,
find-references, etc. IDEs and LSPs do something similar, but more
advanced and requiring a bulky runtime (or multiple runtimes, in the
case of LSPs). Ctags, on the other hand, is a standalone binary that
needs nothing other than the source code text. As a result, it's
significantly faster but at the cost of accuracy.

Why [GNU Global](https://en.wikipedia.org/wiki/GNU_GLOBAL)? Universal
Ctags by itself is just a tag generator. You need something else to go
with it, like editor plugins or a search engine. GNU Global is a code
comprehension tool that can use Universal Ctags as a backend for
tagging. There are many modern code analysis/navigation/search tools
out there, like Sourcegraph or [Google's excellent Code
Search](https://cs.opensource.google/go/go/+/master:src/). But we want
something that can run locally so that our editors can use it. It's
also nice to be able to use semantic code analysis in our own scripts,
e.g., to automate refactoring or to perform complex queries. You can
check the available offerings, but I think GNU Global offers the best
tradeoffs, being lightweight (mostly C) and
[feature-rich](https://github.com/oracle/opengrok/wiki/Comparison-with-Similar-Tools).

# Install Universal Ctags

[Universal Ctags](https://github.com/universal-ctags/ctags)

Wherever you install it, make sure it is on your PATH as `ctags` and this is the output of `ctags --version`:

```bash
Universal Ctags 6.1.0, Copyright (C) 2015-2023 Universal Ctags Team
Universal Ctags is derived from Exuberant Ctags.
Exuberant Ctags 5.8, Copyright (C) 1996-2009 Darren Hiebert
  Compiled: Jul 23 2024, 05:15:30
  URL: https://ctags.io/
  Output version: 0.0
  Optional compiled features: +wildcards, +regex, +gnulib_fnmatch, +gnulib_regex, +iconv, +option-directory, +xpath, +json, +interactive, +yaml, +case-insensitive-filenames, +packcc, +optscript, +pcre2
```

It is unfortunate that the name `ctags` conflicts with several
different programs—some abandoned (Exuberant Ctags) and Emacs's
bundled `ctags`. So this step is necessary. Edit your shell PATH if
necessary. You will need this for the next step.

# Install GNU Global

You can get it from your favorite package manager. (But make sure the package's binary is built with `--with-universal-ctags`. As of writing, Homebrew's version does this but not all Linux package managers do, so you may want to compile your own.)

Or you can build it from source by downloading the latest source archive from the [GNU ftp site](https://ftp.gnu.org/pub/gnu/global/):

```
curl -LO https://ftp.gnu.org/pub/gnu/global/global-6.6.13.tar.gz
tar -xf global-6.6.13.tar.gz
cd global-6.6.13
./configure --with-universal-ctags=$(which ctags)
sudo make install
```

Note `$(which ctags)`—make sure this points to the Universal Ctags binary.

# Configure GNU Global

You'll want to set up your `.globalrc` (a config file that Global looks for) so that Global always uses Universal Ctags.

We'll need a script in the source tree of GNU Global:

```bash
curl -LO https://ftp.gnu.org/pub/gnu/global/global-6.6.13.tar.gz
tar -xf global-6.6.13.tar.gz
cd global-6.6.13
perl ./plugin-factory/maps2conf.pl $(which ctags) '$libdir/gtags/universal-ctags.la' > ~/.globalrc
```

# Using GNU Global

## Emacs

I recommend the excellent [`ggtags-mode`](https://github.com/leoliu/ggtags) package.

## Command line

From any directory with source code, simply run `gtags` and then you can run queries on the tags. Example:

```bash
$ global --result=ctags-x --regexp='filetime_to_timespec'
filetime_to_timespec   77 src/filesystem/time_utils.h inline TimeSpec filetime_to_timespec(LARGE_INTEGER li) {
filetime_to_timespec   84 src/filesystem/time_utils.h inline TimeSpec filetime_to_timespec(FILETIME ft) {
filetime_to_timespec   66 test/std/input.output/filesystems/fs.op.funcs/fs.op.last_write_time/last_write_time.pass.cpp static TimeSpec filetime_to_timespec(LARGE_INTEGER li) {
```

Much more in the [manpage](https://manpages.ubuntu.com/manpages/focal/en/man1/global.1.html) and [official tutorial](https://www.gnu.org/software/global/globaldoc_toc.html).

## Web interface

A cool feature of Global is how it can build an HTML view for the tags, so you can view the code and search for tags in a web browser.

To try it, just run `htags` in a directory with `gtags` files already created and open the generated `HTML/index.html`.
