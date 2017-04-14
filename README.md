* Anything on the JVM
	* Java
	* Scala
	* Clojure
	* Groovy
	* Kotlin
	* JRuby
	* Jython
* Go
* PHP
* Python
* NodeJS
* Haskell


The languages with the seemingly **best tools** as of now are Go (tool developed by Uber) and Java (tool developed by Netflix).  


# Who are Flame Graphs not for?

## Program Types
GUI/Frontend programs that are not widely used and where most of the time is spent waiting on user input.

Small services - optimization has a smaller return when not done at scale. 

## Costs
If running your web service costs an inconsequential annual amount, it's likely not worth your time to profile the service for inefficiencies.

# How are flame graphs useful to software engineers?

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


# Test Systems

## Good canidates we won't be profiling

### Open-Source Distributed Systems

These would all be great canidates for profiling - they have streaming data, perform pretty hefty computations, and are done at scale. Unfortunately, these all seem to be C++ code. At the present time, C++ code is not easy to profile and generate flame graphs for. It has been done, but the tooling does not seem complete.

The systems we could have profiled here include:

* [SETI@home](http://setiathome.ssl.berkeley.edu/)
* [Folding@home](https://folding.stanford.edu/)
* [Bitcoin](https://bitcoin.org/en/)

## Systems we can easily profile

### Program Choosing Criteria

The obvious candidates are any web company's server backend, but those are not open source, so we are targeting anything that meets the follow criteria:

* Easy to profile language
* Scalable services
	* Web servers and anything with a continuous data stream
* Continuously running programs
	* We can get more data points to generate the flame graph
	* Even if it is a GUI program, for the purposes of education it will work nicely

### Program Candidate List

Note that we will not be profiling all of these, but rather those that are easiest to set up and build from source.

* [Minecraft servers](https://hub.spigotmc.org/jenkins/job/BuildTools/)
	* Java
	* Program at scale
	* Continuously running service
	* Streaming data input
* [Docker](https://www.docker.com/)
	* Go
	* Program at scale (with its userbase)
	* Continuously Running
* [iTrace](https://github.com/YsuSERESL/iTrace)
	* Java
	* Continuously Running
	* Program at scale (eventually)
	* Could also include profiling Eclipse itself
* [NASA World Wind](https://github.com/NASAWorldWind/WorldWindJava)
	* Java
	* Continuously Running
	* Will give us interesting GUI oriented results
* [Atom](https://github.com/atom/atom)
	* NodeJS
	* Scale through user base
* [Eclipse Che](https://github.com/eclipse/che/)
	* Java
	* Can be done at scale since it is a web server
* [Google TensorFlow ML Models](https://github.com/tensorflow/models)
	* Python
	* Not continuous running
	* Scale through expensive computations
* [Syncthing](https://github.com/syncthing/syncthing/)
	* Go
	* Scalable by syncing more files
* [Meld](https://github.com/GNOME/meld)
	* Python
	* Optimizations will increase program speed and developer productivity (scalable)
	* Large files with significant diff (scale)
