The FLReconstruct Application
=============================

\tableofcontents

Introduction {#intro}
============
FLReconstruct's task is to read data from an output file generated by
the SuperNEMO simulation or detector, perform reconstruction on each event
in the data, and write the reconstructed data to and output file.
It uses a pipeline architecture for event processing, the pipeline
is constructed as a sequence of "modules", the sequence of modules being
selected by the user (i.e. you) at runtime. Falaise provides a standard
set of modules, and you can write you own custom modules which
FLReconstruct can load at runtime via a plugin mechanism.

Here we present a brief overview of running FLReconstruct from the
command line, including examples of scripting the pipeline using builtin
modules. The more advanced topic of writing and using your own custom
modules is covered in [Writing FLReconstruct Modules](md_WritingFLReconstructModules.html).

Example Usage {#examples}
=============
The flreconstruct program is a command line application just like any
other Unix style program (e.g. `ls`).

Trivial Pipeline {#trivial_pipeline}
----------------
If you do not supply a pipeline configuration script, then `flreconstruct`
will run a dumb pipeline that simple dumps each event to stdout.

We can reproduce this behaviour using the following simple script:

\include flreconstruct/SimplePipeline.conf

The script is formatted as a `bayeux::datatools::multi_properties` ASCII
file.

Creating a Chained Pipeline {#chain_pipeline}
---------------------------
A pipeline with one module isn't very useful! In most cases we want to
plug together a sequence of modules, each performing a well defined
task on the event data.

\include flreconstruct/ChainPipeline.conf

Multi-Module Pipeline {#multi_pipeline}
---------------------
A full chain pipeline can chain together 1 < N < X number of modules.
The previous example showed the basic construct of a chained pipeline
with a single module. We can of course go further and add another module
to the pipeline:

\include flreconstruct/AdvancedChainPipeline.conf

The order in which the modules are processed is determined by the
order in which you list them in the `modules` key of the `dpp::chain_module`
configuration. Try swapping the order to see what happens, and also try
adding further dump modules to the pipeline to experiment with the
sequence.
