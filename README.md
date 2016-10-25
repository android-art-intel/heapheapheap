# heapheapheap
HeapHeapHeap: Am Android native heap tracker

## Introduction

Heapheapheap is a sampling-based, Android native heap tracker. It tracks the memory usage of an application, and reports the corresponding memory hotspots with their backtraces and symbols in a timeline view. That way, it is possible to observe how memory footprint evolve over time, and understand the memory behavior of an application. Heapheapheap uses the same output as common tools that are available in the Linux environment, including Heaptrack and Massif, which is one subtool of the valgrind toolsuite. Therefore, it takes advantage of existing GUIs for vizualisation purposes.

## Launch Heapheapheap tracker on a given app

./heapheapheap com.myprogram.foo

Heapheapheap will take snapshots every two seconds using Android's native heap dumper, called "dumpheap".
If the input program is not started when Heapheapheap starts, it will wait for it to start.
If the input program comes to an end, Heapheapheap will stop its tracking automatically.
Note: At first launch, Heapheapheap will ask you to pull symbols from the device, because it will need them in the parsing phase.

## Heapheapheap parser

Once the program ends, there will be dumps stored on the device. Heapheapheap includes a parser which will fetch, parse and transform the dumps into a form that is more suitable for visualization. It takes the name of the output file you want.

./heapheapheap_parse output.massif

Note: The parser will in fact generate two files:
- output.massif: Generates a file that can display the hotspots
- output.massif.details: Same output as first, but also adds additional information, including number of backtrace calls, and percentage of total memory consumption. This breaks the chart display in the visualizer, hence we want to keep both formats separated for now.

## Visualization of Heapheapheap output

Heapheapheap uses a standard output that is used by valgrind and Heaptrack, that are common tools of the Linux environment. For this example, we are using Massif-Visualizer, an open-source visualizer. 

massif-visualizer output.massif

The GUI shows nicely the different snapshots, as long with their corresponding backtraces and resolved symbols, that are ordered by their memory footprint.

![snapshot4](https://cloud.githubusercontent.com/assets/18188676/19678191/f1f75194-9ac6-11e6-9105-cecf7a3cdf7a.png)



