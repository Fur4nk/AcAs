# AcAs
GPU-accelerated asynchronous cellular automaton simulator using OpenCL


Introduction
============

The purpose of this work is to create a simulator for synchronous,
asynchronous, and probabilistic cellular automata. Cellular automata are
a powerful modeling tool for physical and biological phenomena;
for this reason, we set out to create a simulator that
can handle multiple types of cellular automata, suitable for
these kinds of simulations.

The desire to simulate biological phenomena has led to the need to
use variants of cellular automata better suited for these
simulations, as biological systems are inherently asynchronous. One of these
variants, asynchronous cellular automata (ACA), was introduced for this
purpose, and its implementation represents one of the main innovative
aspects of the simulator.

Since cellular automata are a widely used model, several simulators
already exist. However, these simulators suffer from several problems that make
them unfit for biological simulations. In particular, they do not
handle asynchronous cellular automata and do not support
simulations with large amounts of data. Most current simulators
are not multi-platform, are unable to exploit all the
available hardware such as graphics processing units (GPUs), and are
usually single-threaded.

The objective of this work was therefore to develop a simulator that:

-   Can simulate inherently asynchronous biological
    phenomena, through the support of
    asynchronous cellular automata.

-   Is portable across operating systems.

-   Can properly exploit the hardware of modern computers.

-   Can run simulations with large amounts of data.

-   Gives the user the ability to define local rules without
    restrictions.

-   Can perform simulations in one, two, or three
    dimensions.

A simulator with the features listed above can effectively model
phenomena for which cellular automata representations exist.


How To Use
==========

COMING SOON!


Cellular Automata
=================

A cellular automaton can be seen as a set of cells arranged on a
lattice. Every cell has a state taken from a finite set. At each
iteration all cells are updated synchronously according to their state
and the state of a finite number of neighboring cells using a local rule
common to all cells. The dynamics of cellular automata can be very
complex even for simple local rules. For this reason they are a
complement to differential equations as a tool for modeling physical and
biological phenomena.


![Example of cellular automata](images/rule30.png)

The automata just described are classical cellular automata, in which all
cells are updated simultaneously. In addition to classical cellular
automata, there are variants that we have chosen to support, which are
interesting beyond theory alone. In particular:

-   Probabilistic: each cell is updated depending on a fixed
    probability $p$.

-   Asynchronous: the update is completely asynchronous; at each
    iteration only a single cell is updated.

Both variants are important because they enable the simulation
of non-synchronous systems. In fact, they are commonly used
to model natural phenomena.

Computation on GPUs
===================

We have chosen to leverage GPU computation, specifically through
*OpenCL* (*Open Computing Language*), so that
large amounts of data can be processed more
efficiently.

GPGPU (*General-Purpose computing on
Graphics Processing Units*) was born around the year 2000, when
researchers began to use GPUs for general-purpose
computation. They realized that the computing power of GPUs could
significantly improve the performance of many scientific applications.

As GPU architectures evolved, OpenCL was created as a
framework for GPU programming in C++. This framework
simplifies development and allows harnessing the computing power of GPUs.

OpenCL was designed to take advantage of GPU hardware, but it can also be
used on CPUs (when a compatible GPU is not available).

The performance gap between CPUs and GPUs stems from the fact that,
being designed for rendering, GPUs are
specialized for highly parallel and computationally intensive operations.

Due to the inherently parallel nature of *cellular automata*, we can take
full advantage of GPU parallelism.

Comparison with other simulators
================================

The simulator was compared with the most widely used general-purpose *CA*
simulators, excluding those designed for the study of a
single phenomenon. The existing simulators are weak in at least one of
the following aspects:

-   Low portability.

-   They support only a restricted set of rules.

-   Difficulty in performing simulations with large amounts of data.

-   They do not adequately exploit the available hardware of
    modern computers.

-   They cannot simulate non-synchronous variants of classical
    cellular automata.

-   They can operate in only one or two dimensions.

The simulator aims to achieve the following goals: managing cellular automata
variants suitable for the simulation of natural phenomena (asynchronous
and probabilistic automata), being multi-platform, supporting
any user-defined rule, operating on very large data sets, being easily
extensible, and being able to exploit current hardware
architectures. These are the characteristics that set it apart
from existing simulators. It was compared with two popular simulators
(JCASim and Mirek's Java Cellebration), analyzing their respective strengths and
weaknesses.

Structure of the simulator
==========================

The simulator is designed to run in batch mode; the user controls its
operation via a configuration file. The simulation results are then
stored in one or more output files. The output files of
three-dimensional simulations can be processed by a *Perl* script that,
using a *ray tracing* tool (POV-Ray), can generate images and
movies of the simulations.

More specifically, the structure of the simulator is mainly hierarchical
and modular. The three different types of automata — *Synchronous,
Probabilistic, Walk* — are derived from a single class, *Simulator*. Each of
the three classes has three sub-classes corresponding to the different
dimensions in which simulations can be performed. The simulator was
designed to simplify maintenance and the addition of new types of
cellular automata.

An important feature offered by the simulator is the computation of
submatrices. This is useful for very large universes with few
active cells: in this case, the simulator can operate only on
the relevant blocks, saving time and resources during execution.

![t=2](images/002.png) ![t=10](images/010.png) ![t=18](images/018.png)

Conclusions and Future Developments
===================================

A simulator capable of running classical, asynchronous, and probabilistic
cellular automata has been developed. It works on a wide range of
machines, fully exploiting the available hardware. The simulator was
developed to address needs not covered by other simulators, such
as the ability to work on large data sets in batch mode
without being overly complex for the end user. The ability to
handle non-classical cellular automata, often used for modeling
physical and biological phenomena, is another important feature.

Possible future developments of this project include:


-   Adding a graphical interface for users who do not want to
    run simulations in batch mode.

-   Adding a compression algorithm for the output, which
    would speed up writing to disk.

-   Supporting other types of cellular automata (e.g., CA with non-uniform
    local rules).

-   Providing tools to collect statistics from the simulation.

-   Improving memory management to increase the maximum simulation size.

-   Developing precompiled functions to assist the user in writing
    rules.

A graphical interface would facilitate input specification and
output visualization.

A compression algorithm for the outputs (and decompression for the
inputs) would help reduce the bottleneck caused by
writing to disk. It would be interesting to implement this functionality
using *OpenCL*.

It may also be necessary to add new types of cellular automata. It would
be useful to add a tool for collecting simulation statistics,
such as the number of cells in a given state at each time step.

A more detailed study of memory usage could lead to a reduction in
consumption and consequently an increase in the maximum size of the
simulated systems.


