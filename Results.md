| [Description](README.md) | [Use Cases](UseCases.md)| Results | [Setup](Setup.md) | [Run](Run.md) | [Evaluation](Evaluation.md)

# Results

## Folding@HOME

"Folding@home (FAH or F@h) is a distributed computing project for disease research that simulates protein folding, computational drug design, and other types of molecular dynamics." - [Wikipedia](https://en.wikipedia.org/wiki/Folding@home)

Thousands of people have Folding@home installed on their PCs to try 

50.63% of the execution time was spent in a library called [Gromacs](https://redmine.gromacs.org/) which is used to simulate Newtonian physics for millions of particales in macro biomolecules, especially protiens.

Great, we pass the santity check, we are spending the majority of our time doing something that sounds like our main task. The question is what are we doing with the remaining 50% of the time?

## VDI ext2 file utitility

## Syncthing

Syncthing is a consumer file synchronization tool for consumers that uses a propriety distributed peer-to-peer block protocol to sync data between PCs. Essentially, Syncthing keeps folders you choose up to date on an arbitrary number of PCs without the use of a central sync server.

Syncthing is written in Go and these results were created with Uber's go-torch tool. Syncthing's developer team seems to be quite good and organized, and they actually already had Go's pprof profiling tool enabled, all I had to do was create a bash variable with the address and port I wanted the profiler to use.

### Profiling Adding a Sync Directory

When adding a folder to Syncthing the first thing it must do is create a SHA256 hash of every file in the directory to track changes. This is an inheritently CPU intensive task. The results of this are included in the the [Scan New Folder](Flame Graphs/syncthingScanFolder.svg) flame graph linked here.

You can see that the majority of CPU time is spent in Go's SHA256 library. The questions here for Syncthing developers are can anything outside the hash function be optimized and is Go's SHA256 implementation efficient?

### Profiling Syncthing's Sync Operation

I wasn't really sure what to expect here for CPU time - maybe encryption, creating blocks, state synchonization between clients, etc.

As we can see in the [Sync Folder](Flame Graphs/syncthingSyncFolder.svg) flame graph, the majority of time is spent generating summaries. These summaries are likely used for the percentage complete and state synchonization between clients.





The following are examples of results obtained using Flame Graphs:

[FG1](1.svg)

[FG2](2.svg)

[FG3](3.svg)

[FG4](4.svg)
