+++
title = 'How to Build Signal Desktop on Linux'
date = 2020-03-09T00:30:08-07:00
draft = false
+++

Signal offers runnable .deb packages for Debian-based Linux (including Ubuntu among others). For other distributions, there aren't any runnable binaries. There also aren't (or I couldn't find) documentation on how to build it. Here is how I built Signal Desktop on Fedora 31 (x86_64 gnu/linux) as an AppImage executable, which runs easily on any distribution.

Clone the repository.

```bash
git clone https://github.com/signalapp/Signal-Desktop.git && cd Signal-Desktop
```

Change package.json to also build an AppImage,

```
       "node_modules/sharp"
       ],
       "target": [
-        "deb"
+        "deb",
+        "AppImage"
       ],
       "icon": "build/icons/png"
     },
```

Then build it:


```bash
nvm use
npm install --global yarn
yarn install --frozen-lockfile
yarn grunt
yarn icon-gen
yarn build:webpack
yarn bulid-release
```

Your AppImage will be in release/. You can add this to your PATH; e.g. like what I did:

```bash
    ln -s $(pwd)/release/Signal-*.AppImage ~/.local/bin/signal_desktop
```

This works as of April 2020. I guess if you want to guarantee this guide works for you, checkout commit 9c3196a90ce977222d413a9ee0f553ec2aee8a39.
