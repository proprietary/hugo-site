+++
title = 'Unicode Symbols for Social Media'
date = 2019-03-23T01:38:14-07:00
draft = false
+++

## What this is for
This is a list of Unicode symbols / code points that are often used on social media---besides emojis, which are already easy to input.

The symbols themselves are listed alongside their hexademical Unicode code points. For often-used symbols, it’s useful to memorize the numerical code points so that you can input them without having to search engine the symbol (or refer to a webpage like this, which you should bookmark!).

On *Microsoft Windows, macOS, and X11 (GNU/Linux or *BSD)*, [inputing Unicode symbols by their code points](https://en.wikipedia.org/wiki/Unicode_input#Hexadecimal_input) is easy with support for native keyboard shortcuts.

In *Emacs*, `M-x insert-char`.

On *Android or iOS*, as of the time of writing, there is no native equivalent to doing this; you have to use a third-party app or copy/paste from a webpage *like this* (so bookmark it maybe? 😄).

## Bullets
- • – #0x2022 – bullet
- ● – #0x25cf – black circle
- · – #0xb7 – middle dot
- ☉ – #0x2609 – sun
- ◆ – #0x25c6 – black diamond
- ◈ – #0x25c8 – white diamond containing black small diamond
- ❖ – #0x2756 – black diamond minus white x

## Asterisks
- ✱ – #2731 – heavy asterisk
- ⁕ – #0x2055 – flower punctuation mark
- ❋ – #0x274b – heavy eight teardrop-spoked propeller asterisk
- ✻ – #0x273b – teardrop-spoked asterisk
- ✽ – #0x273d – heavy teardrop-spoked asterisk
- ❃ – #0x2743 – heavy teardrop-spoked pinwheel asterisk
- ✿ – #0x273f – black florette
- ❊ – #0x274a – eight teardrop-spoked propeller asterisk

## Punctuation
- — – #0x2014 – em dash
- – – #0x2013 – en dash
- ━ – #0x2501 – box drawings heavy horizontal
- ❝ – #0x275d – heavy double turned comma quotation mark ornament
- ❞ – #0x275e – heavy double comma quotation mark ornament
- … – #0x2026 – horizontal ellipsis
- ® – #0xae – registered sign
- © – #0xa9 – copyright sign
- ™ – #0x2122 – trade mark sign
- ❘ – #0x2758 – light vertical bar

## Arrows
- ← – #0x2190 – leftwards arrow
- → – #0x2192 – rightwards arrow
- ⇒ – #0x21d2 – rightwards double arrow aka “implication arrow”
- ↞ – #0x219e – leftwards two headed arrow
- ⇠ – #0x21e0 – leftwards dashed arrow
- ⇐ – #0x21d0 – leftwards double arrow
- ◄ – #0x25c4 – black left-pointing pointer
- ➞ – #0x279e – heavy triangle-headed rightwards arrow
- ➜ – #0x279c – heavy round-tipped rightwards arrow
- ➠ – #0x27a0 – heavy dashed triangle-headed rightwards arrow
- » – #0xbb – right-pointing double angle quotation mark
- ⫸ – #0x2af8 – triple nested greater-than
- ➼ – #0x27bc – wedge-tailed rightwards arrow
- ➺ – #0x27ba – teardrop-barbed rightwards arrow
- ➤ – #0x27a4 – black rightwards arrowhead
- ► – #0x25ba – black right-pointing pointer
- ➥ – #0x27a5 – heavy black curved downwards and rightwards arrow
- ⇢ – #0x21e2 – rightwards dashed arrow
- ➳ – #0x27b3 – white-feathered rightwards arrow
- ↳ – #0x21b3 – downwards arrow with tip rightwards

## Circled numbers
- ⓪ – #0x24ea – circled digit zero
- ① – #0x2460 – circled digit one
- ② – #0x2461 – circled digit two
- ② – #0x2461 – circled digit two
- ③ – #0x2462 – circled digit three
- ④ – #0x2463 – circled digit four
- ⑤ – #0x2464 – circled digit five
- ⑥ – #0x2465 – circled digit six
- ⑦ – #0x2466 – circled digit seven
- ⑧ – #0x2467 – circled digit eight
- ⑨ – #0x2468 – circled digit nine
- ⑩ – #0x2469 – circled number ten
- ⑪ – #0x246a – circled number eleven
- ➊ – #0x278a – dingbat negative circled sans-serif digit one
- ➋ – #0x278b – dingbat negative circled sans-serif digit two
- ➌ – #0x278c – dingbat negative circled sans-serif digit three
- ➍ – #0x278d – dingbat negative circled sans-serif digit four
- ➎ – #0x278e – dingbat negative circled sans-serif digit five
- ➏ – #0x278f – dingbat negative circled sans-serif digit six
- ➐ – #0x2790 – dingbat negative circled sans-serif digit seven
- ➑ – #0x2791 – dingbat negative circled sans-serif digit eight
- ➒ – #0x2792 – dingbat negative circled sans-serif digit nine
- ➓ – #0x2793 – dingbat negative circled sans-serif number ten

## Extra: Python to generate these lines
You think I manually wrote all this?

```python
    #!/usr/bin/env python3
    
    import unicodedata
    
    def unicode_description(src):
         n = ord(src)
         h = hex(n)
         name = unicodedata.name(src).lower()
         return f"{src} – #{h} – {name}"
    
    def print_unicode_descriptions(s):
         "Paste a string of a bunch of Unicode symbols as input"
         s = s.split()
         for ch in s:
             print("- " + unicode_description(ch))
```
