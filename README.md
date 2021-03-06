# yates-hennel-gen

In this repo I have implemented a generalization of the Yates and Hennel algorithm.

## Method

The [Yates-Hennel paper](https://github.com/bblodfon/yates-hennel-generalization/blob/master/doc/Yates-Hennel%20paper.pdf) presents an algorithm for **full branch coverage testing of any program**.

The implementation of the simple *Yates-Hennel algorithm* would choose one arbitrary forward tree from
the *Decision-to-Decision (DD) graph* and a backward one and then it would calculate `n-m+1` paths based
on the shortest paths of those trees and the formula that is being presented on the paper.
This method can produce paths that are maybe non-coverable or don't reach *100% brach-coverage* (Test Effectiveness Ratio - **TER2 = 1**).

My algorithm is an extension of the *Yates-Hennel algorithm* in the sense that it produces all the sets of solution result paths from every combination of forward and backward trees. (DD-graph is actually a multigraph so that's why there can be many forward and backward trees).

**Having every possible solution path set** (with the addition of being able to remove paths that you know beforehand that are non-coverable and also removing solution path sets that are permutations of others) **you can easily find the best one in terms of TER2 coverage**.

## Compile and run (Windows)

```
g++ -std=c++11 hennel.c -o hennel.exe
hennel.exe < findroot.txt
```

## Notes

- The `.txt` files have *Basic Block graphs* that represent simple programs: `1 2 3` in one line translates to 2 edges: `1->2` and `1->3`.
- The `excluded_paths.txt` has the number of paths excluded and the path themselves (you can change them as you like).
- The `results.txt` is the file where all the results are stored (and some other info, like number of forward trees, etc.)
- The `hennel_graphs` directory has some graphs created (based on the `triangle.txt` file) with the use of the `dot` program.
