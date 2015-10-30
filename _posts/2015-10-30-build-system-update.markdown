---
layout: post
title: "Updating the build system"
data: 2015-10-30 18:35:00
categories: monkey2 update
---

In preparation for 'makelibs' I've spent the last few days rearranging the build system so each app gets it's own build dir. Boring, fiddly stuff, but necessary.

I'm using a .build dir system similar to monkey1's, with a subdir for each 'profile' that will contain the output app, and a build_cache dir for temporary link files, eg:

<pre>
bumptest.monkey2
bumptest.buildv001/
    emscripten/
        bumptest.html
        bumptest.js
        bumptest.data
    desktop_windows_release/
        bumptest.exe
        assets/
    build_cache
        emscripten/
            bumptest.o
        desktop_windows_release/
            bumptest.o
</pre>

Some of this will eventually be configurable, via settings such as PRODUCT_DIR, PRODUCT_NAME etc.

A 'profile' in this case is just a combination of 'build flags', eg: target; debug/profile/release; static/dynamic etc. It'd also be nice to allow people to add custom profiles in addition to the built-in/default ones. Custom profiles would be to define and override compiler and linker options.

Already, just giving each app it's own build dir is giving me a better idea of how monkey2 builds should perform in practice, and once the initial 'build everything' is done, it's looking pretty good!

Bye  
Mark
