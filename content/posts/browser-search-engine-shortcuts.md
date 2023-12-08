+++
title = 'Search Engine Shortcuts for Chromium-based Browsers'
date = 2023-12-08T14:42:54-08:00
draft = false
+++

Whenever I set up a new browser, I always have to copy over the custom search engines (at [`chrome://settings/searchEngines`](chrome://settings/searchEngines)) because for some reason, Import/Export User Settings doesn't include these. There are [ways](https://stackoverflow.com/a/50871650) to import and export these from the filesystem in an internal sqlite database that Chrom{e,ium} uses, but it's not guaranteed to work in the future.

The "Shortcut"s are just my personal choices; use whatever you can remember. This document is mostly for my personal reference.

| Search engine        | Shortcut   | URL with %s in place of query                                                             |
|----------------------|------------|-------------------------------------------------------------------------------------------|
| `cppreference`       | `:cxx`     | `https://en.cppreference.com/mwiki/index.php?title=Special:Search&search=%s`              |
| `Wikipedia (en)`     | `:w`       | `https://en.wikipedia.org/w/index.php?title=Special:Search&search=%s`                     |
| `Wiktionary (en)`    | `:d`       | `https://en.wiktionary.org/w/index.php?title=Special:Search&search=%s`                    |
| `Python3 docs`       | `:py`      | `https://docs.python.org/3/search.html?q=%s`                                              |
| `Yahoo! Finance`     | `:yf`      | `https://finance.yahoo.com/quote/%s?&.tsrc=fin-srch`                                      |
| `YouTube`            | `:yt`      | `https://www.youtube.com/results?search_query=%s&page={startPage?}&utm_source=opensearch` |
| `Github Code Search` | `:gh:`     | `https://github.com/search?q=%s&type=code`                                                |
| `NixOS packages`     | `:nixpkgs` | `https://search.nixos.org/packages?query=%s`                                              |
| `NixOS wiki`         | `:nixwiki` | `https://nixos.wiki/index.php?search=%s`                                                  |
| `ArchWiki`           | `:arch`    | `https://wiki.archlinux.org/title/Special:Search?search=%s`                               |
| `I'm Feeling Lucky`  | `!`        | `https://duckduckgo.com/?hps=1&q=%5C%s&ia=web`                                            |
| `ports.macports.org` | `:ports`   | `https://ports.macports.org/search?q=%s&name=on`                                                                                        |



