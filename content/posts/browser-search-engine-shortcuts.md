+++
title = 'Search Engine Shortcuts for Chromium-based Browsers'
date = 2023-12-08T14:42:54-08:00
draft = false
+++

Whenever I set up a new browser, I always have to copy over the custom search engines (at [`chrome://settings/searchEngines`](chrome://settings/searchEngines)) because for some reason, Import/Export User Settings doesn't include these. There are [ways](https://stackoverflow.com/a/50871650) to import and export these from the filesystem in an internal sqlite database that Chrom{e,ium} uses, but it's not guaranteed to work in the future.

The "Shortcut" works by typing the it in the browser's address bar (such as `:w` for Wikipedia), followed by a space, then your search query. The choices for "Shortcut"s are just my personal preferences. Use whatever you can remember, and you don't need to prefix them with a colon; once again, that's just my preference. This document is mostly for my personal reference.

| Search engine        | Shortcut     | URL with %s in place of query                                                              |
|----------------------|--------------|--------------------------------------------------------------------------------------------|
| `Wikipedia (en)`     | `:w`         | `https://en.wikipedia.org/w/index.php?title=Special:Search&search=%s`                      |
| `Wiktionary (en)`    | `:d`         | `https://en.wiktionary.org/w/index.php?title=Special:Search&search=%s`                     |
| `I'm Feeling Lucky`  | `!`          | `https://duckduckgo.com/?hps=1&q=%5C%s&ia=web`                                             |
| `YouTube`            | `:yt`        | `https://www.youtube.com/results?search_query=%s&page={startPage?}&utm_source=opensearch`  |
| `cppreference`       | `:cxx`       | `https://en.cppreference.com/mwiki/index.php?title=Special:Search&search=%s`               |
| `Python3 docs`       | `:py`        | `https://docs.python.org/3/search.html?q=%s`                                               |
| `Java JDK docs`      | `:jdk`       | `https://docs.oracle.com/en/java/javase/21/docs/api/search.html?q=%s`                      |
| `Github Code Search` | `:gh`        | `https://github.com/search?q=%s&type=code`                                                 |
| `NixOS packages`     | `:nixpkgs`   | `https://search.nixos.org/packages?query=%s`                                               |
| `NixOS wiki`         | `:nixwiki`   | `https://nixos.wiki/index.php?search=%s`                                                   |
| `ArchWiki`           | `:arch`      | `https://wiki.archlinux.org/title/Special:Search?search=%s`                                |
| `ports.macports.org` | `:ports`     | `https://ports.macports.org/search?q=%s&name=on`                                           |
| `Alpine packages`    | `:alpine`    | `https://pkgs.alpinelinux.org/packages?name=%s&branch=edge&repo=&arch=&maintainer=`        |
| `Docker Hub`         | `:dockerhub` | `https://hub.docker.com/search?q=%s`                                                       |
| `X (Twitter)`        | `:x`         | `https://twitter.com/search?q=%s`                                                          |
| `Yahoo! Finance`     | `:yf`        | `https://finance.yahoo.com/quote/%s?&.tsrc=fin-srch`                                       |
| `Crates.io`          | `:crates`    | `https://crates.io/search?q=%s`                                                            |
| `Docs.rs`            | `:docsrs`    | `https://docs.rs/releases/search?query=%s`                                                 |
| `Rust std docs`      | `:ruststd`   | `https://doc.rust-lang.org/std/?search=%s`                                                 |
| `CMake docs`         | `:cmake`     | `https://cmake.org/cmake/help/latest/search.html?q=%s`                                     |
| `Debian packages`    | `:deb`       | `https://packages.debian.org/search?keywords=%s&searchon=names&suite=bookworm&section=all` |
| `Perplexity.ai`      | `:px`        | `https://www.perplexity.ai/search?s=o&q=%s`                                                |
| `Bing`               | `:b`         | `https://www.bing.com/search?q=%s`                                                         |
| `Kubernetes Docs`    | `:k8s`       | `https://kubernetes.io/search/?q=%s`                                                                                        |






