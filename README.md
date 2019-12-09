# Stack Trace Analysis Tool
A Python For parsing and analyzing stack traces. It generates reports for quicker and easier identification od the problems in your application by highlighting the common origin or common consequence.

The main feature of this tool is the aggregation of the stack traces in a hierarchical/sequential way.

The idea came from the article Stack trace analysis for large scale debugging, implementation https://github.com/LLNL/STAT. But instead of doing this across different processes it does this across different stack traces and tries to find common points and represents this a clear visualization. You can quickly see what are the biggest crashes, where do they originate, through which part of the code do they pas, ...

It takes each call as a separate node and tries to build a tree from this by connecting calls that are called between them.

Arnold, Dorian C., et al. "Stack trace analysis for large scale debugging." 2007 IEEE International Parallel and Distributed Processing Symposium. IEEE, 2007.

# Overview
The project is composed of 4 parts. 
- The 1st part is the least important and serves for reading/parsing and forwarding the data into the system. The example reads the data from a CSV file, parses it using Pandas and forwards it to the system. This will have to be implemented for each use case separately.
- The 2nd part is to create an internal structure to aggregate the data in a smaller easier to traverse format. This format will be described in details later. Inspired by  https://github.com/LLNL/STAT
- The 3rd part calculates statistics and internal diagram representations like word cloud or treeMap, etc
- the 4th part covers the visualization. This is probably the most important part and at the same time, the most diverse part as it can be done in a million ways.

## Internal representation - WIP
The internal representation is a directed graph. Where each node represents a specific call in the stack trace. It contains class, method and line number info.

These nodes are then connected to the calls that happened later in a stack trace call. If two different crashes occurred from a common starting point. That starting point node will have 2 children. Each connection will have a weight that represents in cow manny crashes that order occurred.

## Visualizations
### Word cloud
A word cloud visualization is done on the whole text and metadata gathered from the crash reports. The text is cleaned a little bit to remove some of the words that have no meaning in this context. Like word *in, at, true, false, Caused, by, ...*

![Word cloud example](https://previews.123rf.com/images/boris15/boris151507/boris15150700094/42072002-data-corruption-word-cloud-concept-vector-illustration.jpg "Word cloud example")

This can at a really quick glance give some idea what are the most problematic areas. It can also show that there is no one specific problem area.
For example, if the problems in your app are connected wit the purchases, you will probably see a lot of words connected with *iap, purchase, billing, price, ...*

## Treemap
One of the best visualization and also the core visualization of this project is a treemap. This visualization is used a lot in visualizing disk space usage.

With this visualization, you can get a big-picture overview and details at the same time. All the uses and details will be explained later.

![](http://visualizingrights.org/kit/img/treemap.png)


# How to use - WIP

## Treemap
- By concentrating on individual size, you can see what crases cause the most damage
- By concentrating on the top "square" or the square with the most children is can indicate which component needs to be refactored the most
- If there are a lot of children in a parent the issue might be in an unstable parent
- ...