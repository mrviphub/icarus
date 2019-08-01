# icarus

Icarus ICN caching simulator
Icarus is a Python-based discrete-event simulator for evaluating caching performance in Information Centric Networks (ICN).

Icarus is not bound to any specific ICN architecture. Its design allows users to implement and evalute new caching policies or caching and routing strategy with few lines of code.

This document explains how to configure and run the simulator.

Installation
First, ensure that you have Python installed on your machine with version 2.7.9+ or 3.4+.

Then, clone this repository on your local machine and run:

$ make install
This downloads and installs all required dependencies and installs Icarus in editable mode. This means that you can make changes directly on the source code to have effect on your installation.

Usage
You can use Icarus in three different ways:

Run simulations using models provided by Icarus
Process and analyze results from those simulations
Use Icarus modeling tools into your own code.
You can a set of simulations by executing:

$ icarus run --results <RESULTS_FILE> <CONF_FILE>
where:

RESULTS_FILE is the pickle file in which results will be saved,
CONF_FILE is the configuration file describing the experiments to run.
To learn how to set up the configuration file, you may want to look at config.py and possibly modify it according to your requirements. Alternatively, you can look at the examples folder which contains examples of configuration files for various use cases.

Once simulations complete you can print the content of your results file into a human readable format, running:

$ icarus results print <RESULTS_PICKLE_FILE> > <OUTPUT_TEXT_FILE>
Icarus also provides a set of helper functions for plotting results. Look at the examples folder for plot examples.

By executing the steps illustrated above it is possible to run simulations using the topologies, cache policies, strategies and result collectors readily available on Icarus. Icarus makes it easy to implement new models to use in simulations.

To implement new models, please refer to the description of the simulator provided in this paper:

L.Saino, I. Psaras and G. Pavlou, Icarus: a Caching Simulator for Information Centric Networking (ICN), in Proc. of SIMUTOOLS'14, Lisbon, Portugal, March 2014. [PDF], [Slides], [BibTex]

Otherwise, please browse the source code. It is very well documented and easy to understand.

Finally, Icarus provides utilities for modeling the performance of caches and work with traffic traces. The code is included in the icarus.tools package. These tools are described in detail in this paper.

Docker container
This repository contains a Dockerfile that can be used to build a container running Icarus. You need Docker installed on your machine to do so.

You can build a container image with Icarus running:

docker build [--build-arg py=<python-version>] -t icarus .
where python-version is the version of Python you want to use, e.g. 3.6.

You can now spin a container giving you shell access, which you could use to poke around the container and explore the code by running:

docker run --rm -it icarus
Finally you can run any Icarus command with:

docker run icarus <COMMAND>
To run a simulation with Icarus it is advisable to mount in the container the directories where the config file is located and where you intend to store results and access them from the container.

For example, to use config.py and store the result file in the root of the project you could run the container with the following command:

docker run -v `pwd`:/data icarus icarus run -r /data/results.pickle /data/config.py
Development
Running make install creates a fully functional development environment. You can run all test cases with:

$ make test
and build HTML documentation with:

$ make doc
