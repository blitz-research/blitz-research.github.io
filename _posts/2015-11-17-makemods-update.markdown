---
layout: post
title: "Makemods update"
date: 2015-11-17 10:16:00
categories: monkey2 update
---

Alrighty, I finally have what I think is a pretty good module/library system going!

The mx2cc app now has a 'makemod' option in addition to 'makeapp', which creates a '.a' archive file ('.so' to come...) from all .monkey2 files reachable (via #import) from a given root .monkey2 file. For now, you will need to include these source .monkey2 files if you want to redistrubute a module in 'prebuilt' form, but I plan to eventually provide an (optional) way to convert these to a pre-processed format.

The syntax I ended up with for importing a lib is simply #Import "\<libname.monkey2\>". This has a nice symmetry with #Import "localfile.monkey2" and with the existing mechanism where you enclose system lib/framework etc files in "\<\>". In this case, the system file is a precompiled monkey lib.

Libs still currently go in the 'modules' dir, and it might be time to revisit the naming of particular concepts. Currently, 'module' is roughly equivalent to 'monkey source file' but it should probably mean 'precompiled set of .monkey2 files', as it does in bmx. Modules don't have usable names from inside the language (if you want the contents of a module to go into a different namespace, you need to use 'Namespace') so the concept of a 'module' is really only of interest to the compiler anyway.

I was expecting this to be a bit tricky, and indeed it was! While I had the 'guts' of it all going pretty quickly, there was a fairly large fly in the ointment - generics. The problem here is that adding new 'types' of List, Stack, Map etc (eg" List\<Actor\>, List\<View\>...) really means you're changing the 'std' module on the fly, as all these new types end up in the std namespace. But you don't want to have to recompile the std module because of a new generic type, so the source code for these new types has to go in the module they are declared in - which means potential multiple definitions.  

But I think it's all going pretty well now, and solves one of my biggest gripes about monkey1 - the way it had to rebuild everything all the time! Compile times for larger projects should be MUCH better under monkey2 than they were under monkey1.

Bye,  
Mark
