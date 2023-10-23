+++
title = 'Software Stack Preferences'
date = 2023-10-23T07:32:10-07:00
draft = false
+++

These are all **my opinions** on the ideal software stack. I may revise and edit this over time.

## Operating System

## GNU/Linux

Been using it for a decade and can attest to its greatness. But what distro?

**NixOS**

NixOS lets you declaratively state your configuration, which is something sorely lacking. Ever had to manually copy dotfiles, lists of packages installed, etc., to a new machine? Yeah, that's what NixOS solves. `Docker : applications :: NixOS : operating system`. Plus its package manager doubles as a build tool for [reproducible builds](https://en.wikipedia.org/wiki/Reproducible_builds). The Nix family of OS (and this includes Guix) is probably the first real non-incremental advancement in operating systems design since Windows XP.

That said, if you are just starting with Linux, or just want something that is stable and works, I recommend Debian.

## Filesystem

**ZFS**

Since it can run on Linux now with OpenZFS, there's no reason to use anyting else except for special cases. There is no other filesystem with as many man-hours put into it as ZFS, and [it shows](https://openzfs.github.io/openzfs-docs/Basic%20Concepts/RAIDZ.html).

## Shell

**zfs**

## Editor

**Emacs**

## Programming Languages

This is very difficult because you only choose languages for a practical task, and often there is a more or less objectively correct choice of language. Additionally, many of the factors that go into choosing a language, such as library availability and talent availability, depend on [which ones everyone else likes](https://en.wikipedia.org/wiki/Keynesian_beauty_contest). So subjective assessments of languages are irrelevant or even counterproductive, as there is often an objective answer to the question, "Which language should I use?" But I'm going to do it anyway, because this is about my opinion of the *ideal* software stack. 

### Systems

**Rust**

By "systems" I mean low level languages where memory management is deliberate, bare metal I/O is possible, and statements have a clear mapping to generated ASM. Basically anything that you can write an operating system in. So things like C, C++, Ada, Zig, D. C++ is great--probably would bethe practical choice over Rust in 99% of cases for systems programming--but it's full of footguns and isn't even faster than Rust at most benchmarks. The only reason to use C++ over Rust is network effects, i.e., having a bunch of people who know it already and having access to the half a century worth of C++ libraries and tools already made.

### Web

#### Frontend

**TypeScript**

Many many people have tried to dethrone JS. But the only one that succeded was the one smart enough to be a superset of JavaScript. It's the C++ playbook; get adoption through source compatibliity with the most popular language. You could instantly take a JS codebase and turn it into a TypeScript with zero changes. That's powerful for adoption. `C++ : C :: TypeScript : JavaScript`. But the type safety of TypeScript is very welcome. It nearly fixes all the wartsof JavaScript, and it does it all at compile time with virtually no runtime cost--how can you complain?

As for which frontend framework...that changes by the week, so no suggestion there that I would feel confident sticking to. Next.js seems standard though.

#### Backend

**Go**

Go is essentially a DSL for backend web services. It serves that purpose very well. However, "backend" is very broad and can mean a lot of things depending on the type of web application it is. If it's typical, then Go should be more than sufficient.

### Scientific

**Julia**

The other potential choices would be: Python, R, Mathematica, MATLAB/Octave, Fortran. Obviously in practice Python has dominated, just due to numpy/tensorflow/pytorch/pandas, but it is far from an ideal language.

### Formal verification

TODO will add when I learn one

### Hardware

TODO will add when I learn one...probably Verilog

## "General purpose"

**Java**

Or any JVM language. Really, just use the JVM. It is a modern marvel. It is unlikely anything else will catch up to it at this point.

## Academic

**Common Lisp**

Yes, "academic" is a genre of programming language in my view. It's a type of language that is useless but is interesting. And my choice is Lisp. Lisp feels like [the last programming language you'll ever need](https://en.wikipedia.org/wiki/End_of_history), because if you need a domain specific language or a new type of syntax, you can just write a macro.

The alternatives for this category would be things like Haskell, F#, OCaml, Scheme, Racket ...

## Database

**PostgreSQL**
