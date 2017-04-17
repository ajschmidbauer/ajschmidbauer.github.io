| [Description](README.md) | [Use Cases](UseCases.md)| [Results](Results.md) | Setup | [Run](Run.md) | [Evaluation](Evaluation.md)

# C++ Installation Steps

**Disclaimer:** Sorry, no GUI or friendly tools here for C++. The process still is not that difficult once you become familiar with

Flame graph profiling with C++ is actually quite simple, especially if you are familiar with Unix utilities and pipe/filter models. These instructions also work for C programs.

These instructions will only work for Linux, as the methods here have Linux kernel dependencies. There are similar methods described for Windows, Solaris, and OSX on [Brendan Gregg's website](http://www.brendangregg.com/FlameGraphs/cpuflamegraphs.html#Instructions).

## Get the Flame Graph tool

[Brendan Gregg's Flame Graph tool](https://github.com/brendangregg/FlameGraph) is the current defacto tool for digesting stack information and turning it into a visual. The differences all lie in how you acquire the stack information.

The easiest way to get the tool is to clone the git repo:

```git clone --depth=1 https://github.com/brendangregg/FlameGraph.git```

You will want to clone this repo from within a directory that you can use to dump results and work from


## Compile your program correctly

This step is not 100% necessary, but it does help avoid inlined and omitted method names, and makes your results more meaningful.

#### Debug Compiler Flag

The only thing required here is changing the compiler flags. You will want to add ```-g``` if you are building manually, or simiply build from your IDE in the debug configuration to enable debug symbols.

#### Stack Frame Pointer Optimization

Occasionally, g++ will remove or share stack frame pointers and method stacks will be incorrectly reported. To prevent the compiler from doing this, add the followig flag:

```-fno-omit-frame-pointer```

### That's It!

You are now setup and ready to profile your C/C++ application on Linux! Read more in our instructions on profiling and generating flame graphs for C++ programs.


### Source

(Brendan Gregg's Website)[http://www.brendangregg.com/FlameGraphs/cpuflamegraphs.html#Instructions]
