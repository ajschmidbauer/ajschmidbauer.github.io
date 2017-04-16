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

## Run your program and acquire a stack trace

Make sure you are in the same directory used above to clone the FlameGraph repository.

1. Have the program to be profiled running.

2. Begin Profiling:

    ```sudo perf record -F 99 -a -g -- sleep 60```
    
    **About this command:**
    
    ``perf``` is the Linux tool for getting kernel stack traces.
    
    We are running it in ```record``` mode
    
    ```-F 99``` says that we want to gather stacks at a frequency of 99 Hz
    
    ```-a``` says we wil capturing data for all CPUs
    
    ```-g``` says we want call graph (call stack) information
    
    ```--``` is the separator between options and the command
    
    ```sleep 60``` says to record data for 60 seconds
    
    
    The parameters here that you can tune are the frequency and the time to record. Some CPUs have been know to have trouble at values greater than 100 Hz, so try for 99 Hz and below.
    
    
3. Now it's time to dump the profiling results to a file

    We will also combine this step with collapsing the stacks by frequency
    
    ```sudo perf script | ./FlameGraph/stackcollapse-perf.pl > out.perf-folded```
    
    If you see some errors here about "failed to open" or "no symbols found", that is fine, they are not related to the profiling and relate to some other temporary files.
    
    The stackcollapse program takes a file with a list of stacks that looks like:
    
    ```
    stack1
    stack2
    stack1
    stack1
    stack2
    ```
    And then collapses the stacks by frequency to something like:
    
    ```
    3 stack1
    2 stack2
    ```
    
    This makes it easier for the FlameGraph tool to assign a size to each stack.

4. Generate the flame graph

    To see the system-wide flame graph use the command:
    
    ```./FlameGraph/flamegraph.pl out.perf-folded > systemWide.svg```
    
    This svg file can be view in the browser using ```firefox systemWide.svg```
    
    Once you know the reported name of your program (bottom most layer specific to your program), you can filter the stack results with grep.
    It also may be easier to find your program's name by clicking on stacks which will zoom the graph to that area and you can see the results more closely.
    
    
    ```
    grep "MyProgramName" out.perf-folded | ./FlameGraph/flamegraph.pl > myProgramGraph.svg
    ```
    
    Similarly, this can be viewed with ```firefox myProgramGraph.svg```

## Summary

This is the order of commands to be ran:

1. ```git clone --depth=1 https://github.com/brendangregg/FlameGraph.git```
2. Compile with ```-g -fno-omit-frame-pointer```
3. ```sudo perf record -F 99 -a -g -- sleep 60```
4. ```sudo perf script | ./FlameGraph/stackcollapse-perf.pl > out.perf-folded```
5. grep "MyProgramName" out.perf-folded | ./FlameGraph/flamegraph.pl > myProgramGraph.svg
6. firefox myProgramGraph.svg