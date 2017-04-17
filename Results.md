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

Syncthing is written in Go and these results were created with Uber's go-torch tool.

[Scan New Folder](Flame Graphs/syncthingScanFolder.svg)

[Sync Folder](Flame Graphs/syncthingSyncFolder.svg)





The following are examples of results obtained using Flame Graphs:

[FG1](1.svg)

[FG2](2.svg)

[FG3](3.svg)

[FG4](4.svg)
