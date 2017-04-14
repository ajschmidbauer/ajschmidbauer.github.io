| [Description](README.md) | [Use Cases](UseCases.md)| [Results](Results.md) | [Setup](Setup.md) | Run | [Evaluation](Evaluation.md)

# Run

## How should a developer use flame graphs?

1. State the main purpose of your application
	* For example, let's imagine we are the Google Maps backend. We want to do receive some data (address waypoints for instance), do some expensive processing (I imagine routing is non-trivial), and return the route over the network.
2. From your main purpose, make an educated guess about where you expect the majority of CPU time should be spent. This should usually be your application's purpose, not additional serialization or network tasks.
	* For our Google Maps example, we'd probably want 75% or more of our CPU time spent on graph route processing - this seems much more expensive than network communication.
3. Profile your application using your flame graph tool of choice.
	* Different tool for each language so far
4. View the results.
	* Were your assumptions correct? Or are you spending most of your time constructing objects that could be static resources?
	* Also compare different operations. For example, do you spend more time looking up an address than finding a route there? Also, do you spend more time constructing an object than you do using it (especially true of library generated objects)?

## Reading Flame Graphs

These are actually quite simple to read.

![mySQL](./flamegraphmysql.png)

The above image shows MySQL codepaths consuming CPU cycles. The x-axis represents stack profile population (percentage of CPU time for that method), and the y-axis represents stack depth. Each section is a stack frame, with wider sections representing stacks that are present more often. At the top, the edges represent what is on CPU, and beneath them are its ancestors (exactly like a program stack trace). It is important to note that color is not signifigant to the interpretation of the graph, and neither is the sorting order (they are sorted alphabetically). This means that the left to right order of methods does not imply execution order.

This example is from [Brendan Gregg's website](http://www.brendangregg.com/index.html), the creator of Flame Graphs.
