+++
title = 'How to Use Keyboard as Mouse on Linux'
date = 2023-10-27T00:31:23-07:00
draft = false
+++

This is a nice trick. It lets you use your keyboard's numpad as a mouse. I had to use this while troubleshooting a server on a live Linux USB installation which booted up to a KDE Desktop Environment, but I did not have a mouse to go along with it, only a keyboard. I was able to open Konsole, the terminal emulator, and enter the following to activate keyboard mouse keys:

```bash
setxkbmap -option keypad:pointerkeys
```

This, of course, only works on Xorg, not Wayland. So it will probably not work on your Gnome if you are using a recent distro.
