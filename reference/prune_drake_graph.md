# Prune the graph **\[deprecated\]**

2019-01-08

## Usage

``` r
prune_drake_graph(graph, to = igraph::V(graph)$name, jobs = 1)
```

## Arguments

- graph:

  An igraph object.

- to:

  Character vector of vertices.

- jobs:

  Number of jobs for parallelism.

## Value

An `igraph` object
