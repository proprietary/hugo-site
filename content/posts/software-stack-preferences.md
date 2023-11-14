+++
title = 'Ranking tools'
date = 2023-10-23T07:32:10-07:00
draft = false
+++

These are all **my opinions** on the ideal set of software. I may revise and edit this over time.

## Filesystem

**ZFS**

Since it can run on Linux now with OpenZFS, there's no reason to use anyting else except for special cases. There is no other filesystem with as many man-hours put into it as ZFS, and [it shows](https://openzfs.github.io/openzfs-docs/Basic%20Concepts/RAIDZ.html).

Notable runner-ups:

0. btrfs, which is like ZFS but is in the kernel tree
0. [bcachefs](https://bcachefs.org/) which is being merged in kernel 5.7 and is a promising alternative to both ZFS and btrfs (but I'd wait for it to be used for a few years and data recovery tools to be made before switching to it)

## Shell

**zsh**

## Editor

**Emacs**

Emacs works in TTYs / terminals / `tmux(1)` so it will always be in a different category from VSCode and the like.

## Programming Languages

This is very difficult because you only choose languages for a practical task, and often there is a more or less objectively correct choice of language. Additionally, many of the factors that go into choosing a language, such as library availability and talent availability, depend on [which ones everyone else likes](https://en.wikipedia.org/wiki/Keynesian_beauty_contest). So subjective assessments of languages are irrelevant or even counterproductive, as there is often an objective answer to the question, "Which language should I use?" But I'm going to do it anyway, because this is about my opinion of the *ideal* software stack. 

### "General purpose"

**Java**

Or any JVM language like Kotlin. Really, just use the JVM. It is a modern marvel. It balances speed, reliability and ease-of-use in a remarkable way. It is unlikely anything else will catch up to it at this point.

### Systems

**Rust**

Notable runner-ups:

0. C++
0. Zig
0. Ada
0. C

By "systems" I mean low level languages where memory management is deliberate, bare metal I/O is possible, and statements have a clear mapping to generated ASM. Basically anything that you can write an operating system in. So things like C, C++, Ada, Zig, D. C++ is great--probably would bethe practical choice over Rust in 99% of cases for systems programming--but it's full of footguns and isn't even faster than Rust at most benchmarks. The only reason to use C++ over Rust is network effects, i.e., having a bunch of people who know it already and having access to the half a century worth of C++ libraries and tools already made.

### Web frontend

**TypeScript**

You could instantly take exiting JS and convert it into a TypeScript with zero changes. That's powerful for adoption.

`C++ : C :: TypeScript : JavaScript`

### Web backend

**Go**

Go is essentially a DSL for backend web development or web APIs. It serves that purpose very well.

### Scientific

**Julia**

The other potential choices would be: Python, R, Mathematica, MATLAB/Octave, Fortran. Obviously in practice Python has dominated, just due to numpy/tensorflow/pytorch/pandas, but it is far from an ideal language. The problem with Python+numpy is that all the performance-critical code are FFI extensions written in native languages like C++. Then when you want to, say, use a Tensorflow trained model in production, there have to be all these tools to export the model to a binary format that you then run on a C++-based runtime. Python also has the GIL, which still hasn't been solved after all these years, making it impossible to run really high-performance or mission-critical code. So what is Python? It's like a modern BASIC. Julia, on the other hand, is actually capable of producing high-performance software, and its semantics are similar to Lisp, so it's a joy to use in my opinion.

### Scripting

**Ruby**

It has some benefits over Python for typical scripting. See: regular expression operators built-in to the language. It's a good `bash` replacement. Ruby also is unlikely to go away, being an ISO standard. However, Python is better for applications.

### Formal verification

TODO add section when I learn one (e.g., Coq, SPARK)

### Hardware

TODO will add when I learn one...probably Verilog

### Academic

**Common Lisp**

Lisp feels like [the last programming language you'll ever need](https://en.wikipedia.org/wiki/End_of_history), because if you need a domain specific language or a new type of syntax, you can just write a macro.

The alternatives for this category would be things like Haskell, F#, OCaml, Scheme, Racket... None of them are very useful (sadly neither Lisp), but they are interesting nonetheless.

## Database

**PostgreSQL**

## Operating System

Been using GNU/Linux for over decade now and can attest to its greatness. But what distro?

**NixOS**

NixOS lets you declaratively state your configuration, which is something sorely lacking. Ever had to manually copy dotfiles, lists of packages installed, etc., to a new machine? Yeah, that's what NixOS solves.

`Docker : applications :: NixOS : operating system`

Plus its package manager doubles as a build tool for [reproducible builds](https://en.wikipedia.org/wiki/Reproducible_builds). The Nix family of OS (and this includes Guix) is probably the first real non-incremental advancement in operating systems design since Windows XP. It has a chance to become "the final word" in operating systems (on the server-side of course), the same way ZFS is the final word for filesystems.

My ranking of operating systems:

0. NixOS (a Linux distro focused on reproducibility and functional programming concepts)
0. Debian (a versatile, general purpose Linux distro that the most software is compatible with because it is the most popular)
0. MacOS (it literally just works)
0. Qubes OS (a Linux distro focused on security by isolating applications into their own VMs; I'm a fan of any OS that actually comes up with new innovations)
0. Any other GNU/Linux distro. (Gentoo, Arch, openSUSE, Slackware, etc. all fit in here. Good because they are Linux, but not particularly interesting anymore.)
0. OpenBSD (security-focused UNIX; creators of OpenSSH)
0. FreeBSD (unlike Linux which has you mix and match millions of packages for every basic thing, FreeBSD is an all-in-one system with great documentation; only problem is that it's basically abandoned by now)
0. Windows
