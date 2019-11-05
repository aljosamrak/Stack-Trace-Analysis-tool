# Stack Trace Analysis Tool
A Python For parsing and analyzing stack traces. It generates reports for quicker and easier identification od the problems in your application by highlighting the common origin or common consequence.

The main feature of this tool is the aggregation of the stack traces in a hierarchical/sequential way.

The idea came from the article -Stack trace analysis for large scale debugging, implementation https://github.com/LLNL/STAT. But instead of doing this across different processes it does this across different stack traces and tries to find common points and represents this a clear visualization. You can quickly see what are the biggest crashes, where do they originate, through which part of the code do they pas, ...

It takes each call as a separate node and tries to build a tree from this by connecting calls that are called between them.

Arnold, Dorian C., et al. "Stack trace analysis for large scale debugging." 2007 IEEE International Parallel and Distributed Processing Symposium. IEEE, 2007.