+++
title = 'Ranking tools'
date = 2023-10-23T07:32:10-07:00
draft = false
+++

These are **my opinions** on the ideal software stack. I will revise and edit this over time. This is purely for entertainment purposes.

## Filesystem

**ZFS**

Since it can run on Linux now with OpenZFS, there's no reason to use anyting else except for special cases. There is no other filesystem with as many man-hours put into it as ZFS, and [it shows](https://openzfs.github.io/openzfs-docs/Basic%20Concepts/RAIDZ.html).

Notable runner-ups:

0. btrfs, which is like ZFS but is in the kernel tree
0. [bcachefs](https://bcachefs.org/) which is being merged in kernel 5.7 and is a promising alternative to both ZFS and btrfs (but I'd wait for it to be used for a few years and data recovery tools to be made before switching to it)

## Shell

**zsh**

It's close enough to bash that it's easy to pick up, but it fixes a lot of the annoying little problems and limitations of bash.

## Editor

**Emacs**

Emacs works in TTYs / terminals / `tmux(1)`, so it will always be in a different category from VSCode, JetBrains and the like, even though those are fantastic tools.

The next-best choice is neovim. It's definitely more popular than Emacs at this point as the not-an-IDE editor of choice. (Neo)vim is great. I really like the idea of modal editing and prefer to use vim keybindings in Emacs because it's generally faster and less RSI-inducing.

But I prefer Emacs for a few reasons, the main one being Lisp. Emacs is an excuse to use Lisp (I'll admit it). But there is good reason for Lisp. Thanks to the interactive devloop style of writing Lisp, there is a lot less friction in testing new ideas and debugging as you go, allowing you to write a program brick-by-brick. This lends itself very well to using an editor. You typically wouldn't want to spend hours to, say, write a VSCode extension or JetBrains plugin that just helps you add a copyright header to a bunch of files—you'd spend less time doing it by hand, so you'll just do it by hand. In Emacs you can just drop into `*scratch*`, write an Lisp function, evaluate it, and run it; there is virtually no friction. This example just scraches the surface. Emacs is less of an editor and more of a Lisp Machine OS that you can tailor to your specific needs. I used to care a great deal about OSes and Linux distros, but slowly I realize none of that matters as long as I can run Emacs. The OS can be anything—Mac or Windows, too—because it's just a bootloader for Emacs.

Thanks to the [Language Server Protocol](https://langserver.org/) by Microsoft for VSCode, most IDE features can be replicated in Emacs; you just have to install some language servers. Emacs has `eglot` as a built-in client for LSP servers. But why not just use an IDE? You can and should. You can use both. The difference with Emacs is it works for every programming language or markup language that exists or probably will ever exist. Every keybinding you learn or macro you write in Emacs can be taken with you forever, leading to compounding returns in productivity. It's nice to get into a state of flow when writing code or words, and it's much easier when you are not splitting your attention with fighting a new unfamiliar IDE for every language.

There are a number of drawbacks to be aware of, though, in case this has convinced you to start learning Emacs. One place where it falls short is debugging. Emacs has an *okay* frontend for gdb, but of course gdb only works for programming languages like C, C++ and Rust. For languages like Python, Java, Ruby, C#, JavaScript, etc., there's nothing really. (Emacs does have best-in-class support for debugging Lisp, but let's be real, no one cares about Lisp.) Another obvious place where Emacs fails is the insane amount of bad defaults. You will have to spend a lot of time configuring it to be usable.

## Programming Languages

This is very difficult because you only choose languages for a practical task, and often there is a more or less objectively correct choice of language. Additionally, many of the factors that go into choosing a language, such as library availability and talent availability, depend on [which ones everyone else likes](https://en.wikipedia.org/wiki/Keynesian_beauty_contest). So subjective assessments of languages are irrelevant or even counterproductive, as there is often an objective answer to the question, "Which language should I use?" But I'm going to do it anyway, because this is about my opinion of the *ideal* software stack. 

### Systems

**Rust**

The second-best choice is C++, but only if you run asan/tsan/ubsan/valgrind religiously to catch the safety issues. The worst choice is C.

By "systems" I mean low level languages where memory management is deliberate, bare metal I/O is possible, and statements have a clear mapping to generated ASM. Basically anything that you can write an operating system in. So things like C, C++, Ada, Zig, D. C++ is great--probably would be the practical choice over Rust in 99% of cases for systems programming--but it's full of footguns and isn't even faster than Rust at most benchmarks. The only reason to use C++ over Rust is network effects, i.e., having a bunch of people who know it already and having access to the half a century worth of C++ libraries and tools already made. C is just C++ but without any of the expressiveness.

### Web frontend

**TypeScript**

You could instantly take exiting JS and convert it into a TypeScript with zero changes. That's powerful for adoption.

`C++ : C :: TypeScript : JavaScript`

### Web backend

**Go**

Go is essentially a DSL for backend web development or web APIs. It serves that purpose very well. It's also the most simple language ever, which is sometimes a breath of fresh air even if it lacks a lot of the expressiveness of other modern langs.

### Scientific

**Julia**

Obviously in practice Python has dominated, just due to numpy/tensorflow/pytorch/pandas, but it is far from an ideal language. Julia seems like an effort to do it right. It has modern language features. It has metaprogramming. Due to its compiled nature (via LLVM), models written in Julia are efficient enough to be run in production directly, whereas deploying models made in Python requires elaborate tricks (mostly passing the buck to efficient C++ code provided by a framework). Julia can also be used in many scenarios where Python simply can't (thanks to the GIL).

### Scripting

**Ruby**

It has some benefits over Python for typical scripting. See: regular expression operators built-in to the language. It's a good `bash` replacement. Ruby also is unlikely to go away, being an ISO standard.

### Hardware

TODO will add when I learn one...probably VHDL

### General purpose

**Common Lisp**

Lisp feels like [the last programming language you'll ever need](https://en.wikipedia.org/wiki/End_of_history), because if you need some language construct that doesn't exist, you can just write a macro. Lisp is like a language to design your own language geared for your specific problem domain. It was the first (or one of the first) high-level programming languages, and it will probably be the last.

But if Lisp is out of the question, then JVM (any JVM language, but plain Java after 21 is good, too, nowadays). The JVM is a modern marvel, and it's unlikely anything will catch up to it at this point.

## Database

**PostgreSQL**

## Build system

**Bazel**

If you've used a modern build system like Bazel or Buck, stuff like CMake or gradle will seem obsolete.

## Operating System

### Linux distro

Been using GNU/Linux for over decade now and can attest to its greatness. Best distro:

**NixOS**

NixOS lets you declaratively state the configuration of the OS using configuration files written in the Nix language. This unlocks a lot of interesting abilities, such as being able to time-travel to a previous configuration of the OS. It also solves one of the biggest problems in software, which is dependencies.

`applications : Docker :: OSes : NixOS`

Plus its package manager doubles as a build tool for [reproducible builds](https://en.wikipedia.org/wiki/Reproducible_builds). The Nix family of OS (and this includes Guix) is probably the first real non-incremental advancement in operating systems design since Windows XP. It has a chance to become "the final word" in operating systems (on the server-side of course), the same way ZFS is "the final word for filesystems."
