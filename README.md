#  Custom GitHub action
This repository contains a simple implementation of a custom workflow for the project "RcppDeepState" of GSOC 2022.
This package can be used to perfmorm a simple CI task : test the `dijkstraSparseMatrix` function defined in the [Dijkstra](https://github.com/FabrizioSandri/Gsoc-R)  package developed for the easy task.


## Usage 
This package tests the execution of the Dijkstra algorithm on the capital cities graph plotted in the following picture, by calculating the distance vector from a specific soruce node.

![Cities](https://i.postimg.cc/zDpZXg4F/graph.png)

Inputs available
* `source_node` the source node you want to compute the distance vector for the capital cities graph. Example: `Paris`
* `zoneinfo` the timezone path you want to use to setup the docker environment. Example: `Europe/Helsinki`


## Exmaple usage
In the following code sample we are triggering the workflow in case of a `push` or a `pull_request`.
In this particular case the `source_node` is set to `Rome` and the `zoneinfo` is left empty (fallback to the defaul value)

```yaml
on:
  push:
    branches: [main, master]
  pull_request:
    branches: [main, master]

name: custom-check

jobs:
  custom_test:
    runs-on: ubuntu-latest
    env:
      GITHUB_PAT: ${{ secrets.GITHUB_TOKEN }}
    steps:
      - uses: actions/checkout@v2
      - name: Setup R environment and test cities graph 
        uses: FabrizioSandri/Gsoc-RcppDeepState-Medium@main
        with:
          source_node: "Rome"

```
