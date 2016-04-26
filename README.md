# podio

## Bug tracker
Please submit feature requests and bugs to
[https://sft.its.cern.ch/jira/projects/PODIO](https://sft.its.cern.ch/jira/projects/PODIO)

## Documentation

 - [Introduction](./doc/doc.md)
 - [Design](./doc/design.md)
 - [Data Model Syntax](./doc/datamodel_syntax.md)
 - [Examples](./doc/examples.md)
 - [Advanced Topics](./doc/advanced_topics.md)

Browse the API documentation created with Doxygen at 

[http://fccsw.web.cern.ch/fccsw/podio/index.html](http://fccsw.web.cern.ch/fccsw/podio/index.html).

## Prerequisites

If you are on lxplus, all the necessary software is preinstalled.

On Mac OS or Ubuntu, you need to install the following software. 

### ROOT 6.06

Install ROOT 6.06 and set up your ROOT environment: 

    source <root_path>/bin/thisroot.sh

### Python 2.7

Check the python version by doing:

    python --version

Check that the yaml python module is available

    python
    >>> import yaml

If the import goes fine (no message), you're all set. If not, you need to install yaml. For that, you need to:

1- install the C++ yaml library, which is used by the python module. On Mac OS, The easiest way to do that is to use homebrew (install homebrew if you don't have it yet):

    brew install libyaml

2- install the python yaml module (first install pip if you don't have it yet)

    pip install yaml

Check that you can now import the yaml module in python.


## Preparing the environment

Before building and installing this package, and everytime you need to use it, do:

    source ./init.sh


## Compiling

Set up separate build and install areas, and trigger the build: 

    mkdir build
    mkdir install
    cd build
    cmake -DCMAKE_INSTALL_PREFIX=../install ..
    make -j 4 install

To see a list of options, do this in the build-directory:

    cmake -LH ..

## Running

The examples are for creating a file "example.root",

    ../install/tests/write

reading it again in C++,

    ../install/tests/read

and reading it again in python,

    python ../tests/read.py

## Modifying the data model

Podio features an example event data model, fully described in the yaml file
[tests/datalayout.yaml](tests/datalayout.yaml).
The C++ in [tests/datamodel/](tests/datamodel/) has been fully generated by a code generation script, [python/podio_class_generator.py](python/podio_class_generator.py).

To run the code generation script, do

    mkdir ../Tmp
    mkdir ../Tmp/data
    mkdir ../Tmp/src
    python ../python/podio_class_generator.py ../examples/datalayout.yaml ../Tmp data


## Running tests
After compilation and installation (!) you can run rudimentary tests with

    make test
