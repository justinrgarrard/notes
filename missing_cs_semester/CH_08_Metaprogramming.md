---
layout: page
---

# CH 8 | Metaprogramming

> "What do we mean by “metaprogramming”? Well, it was the best collective term we could come up with for the set of things that are more about process than they are about writing code or working more efficiently."

### Build Systems

* A build system automates the steps to produce output (i.e. compiling code, linking libraries, etc.)

* `make` is a common Unix build system

```
Build System Components

    Dependency  A prerequisite that needs to be in place for building
    Target      The output that will be produced
    Rules       Mappings of dependencies to targets
```

```
# Makefile

## Create paper.pdf with prerequisites of paper.tex and plot-data.png
## Use command `pdflatex` w/ input paper.text
paper.pdf: paper.tex plot-data.png
    pdflatex paper.tex

## Create plot-<variable>.png with prerequisites <variable>.dat and plot.py
## Use command `./plot.py` w/ input arguments
plot-%.png: %.dat plot.py
    ./plot.py -i $*.dat -o $@
```

### Dependency Management

```
Semantic Versioning

    <major>.<minor>.<patch>     (1.12.136)

    If a new release does not change the API, increase the patch version.
    If you add to your API in a backwards-compatible way, increase the minor version.
    If you change the API in a non-backwards-compatible way, increase the major version.
```

* **Lock Files** list dependencies as well as the version used in order to maintain a consistent environment.

### Continuous Integration and Testing

* A system that performs changes whenever code is modified (i.e. running a test suite)

```
Common Test Vocabulary

    Test suite          A collective term for all the tests
    Unit test           A “micro-test” that tests a specific feature in isolation
    Integration test    A “macro-test” that runs a larger part of the system to check that different feature or components work together
    Regression test     A test that implements a particular pattern that previously caused a bug to ensure that the bug does not resurface
    Mocking             The replace a function, module, or type with a fake implementation to avoid testing unrelated functionality. For example, you might “mock the network” or “mock the disk”

```
 