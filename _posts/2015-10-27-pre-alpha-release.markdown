---
layout: post
title: "New monkey2 pre-alpha released!"
data: 2015-10-27 12:42:00
categories: monkey2 update
---

Ok, new monkey2 demo time!

As with the last demo, this should be installed along side the latest monkey release as it is still IDE-less. It will also work with the latest free version of monkey.

This is still very much pre-alpha stuff, but it should be border-line usable now and has reached a state where I reckon it's worthwhile getting some feedback on how it's shaping up.

The zip file is available [here](http://www.monkey-x.com/mak/mx2/monkey2_28_Oct_2015.zip). I've also started on a little 'monkey1 to monkey2' doc [here]({% post_url 2015-09-14-monkey1-to-monkey2 %}).

Most monkey1 language features should now be more or less functional (though I have tested some way more than others) and a few of the new monkey2 features are proving to be VERY useful. In particular, I am loving function values and structs! There are some other new features in there, but they have received far less testing and some are very underdeveloped.


There is still no thread support, and I've pretty much discarded any stunt parsing to deal with EOL issues (for now). I'll revisit this later, but right now my priority is to get error handling, line numbering etc working correctly and EOLs complicate this somewhat.

There is quite a bit of module code in there, some of which will be familiar to monkey users, and some of which will be familiar to blitzmax users! However, please consider this stuff to be mainly 'brainstorming' code - I find writing modules to be both an excellent way of debugging the compiler, and trying out freaky ideas. Most of the module stuff will remain in one form or another, but some of it will change as language features are added.

So I still don't recommend writing 'real code' with this version...please!

There is some fairly interesting stuff in the modules though, including:

* A pretty complete implementation of mojo2.

* The return of blitzmax's stream system, where you can specify a 'protocol' when opening a stream.

* A quick 'n' nasty implemnation of a 'zip::' stream protocol, courtesy of the miniz lib. Not cached or anything so woefully inefficient.

* A minimal custom GUI. This will probably be a bit controversial, but it's happening. It already provides a few features I think are sorely missing from monkey, such as easy support for virtual resolutions (including dealing with mouse coords and window resizing) and support for multiple windows (which SDL supports so why not?). These are things that are kind of ugly to do without some sort of 'view' architecture.

* A very simple HtmlView based on the litehtml library. Don't expect to be able to write a browser with this, but for displaying docs/instructions I think it will be very useful.

The 'big picture' is shaping up a bit more now, and my next big job is to work on some sort of 'library' system.

Currently, there is no library system to speak of. Source file changes will automatically trigger a recompile of dependant files, but it's all still just a massive soup of source files at heart. This works pretty well once the 'build cache' has warmed up, but it's already hitting limits. When you switch to a different project, far too much stuff is recompiled (partly due to the generics system) and on Windows at least, linking 100-ish object files is brutally slow.

So it's time to clean up the build system and tackle libraries, and what I'm planning to do here is something like blitzmax's 'makemods'. This will behave similarly to 'makeapp', except the result will be a static .a archive file OR a dynamic .so library. You'll be able to import libraries using something like ```#import "<sdl2.monkey2.so>"``` - or, IDEs could perhaps allow you to select libs and pass them on to mx2cc, ala msvc and c#'s assemblies.

The main idea behind supporting .so libs is to make it possible for monkey2 apps to support plugins, something I think would be useful for both games and game editors. By placing all the GC and memory managment stuff in a single shared .so, it should be possible to pass objects etc around between plugins with no problems (ha!). This is all likely to impact the module archictecture considerably so I think it needs to be done before I get any deeper into module/library development.

Other big picture stuff includes reflection and debugging, but that's a story of another post!

Bye!  
Mark
