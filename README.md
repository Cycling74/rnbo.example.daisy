# RNBO for the Daisy Audio Platform

## Author

Stefan Brunner - stb@cycling74.com

## Description

This should hopefully get you started on using RNBO on the Daisy Audio Platform (https://electro-smith.com/).

First things first: this is under heavy development, so use this at your own risk, it might suddenly crash, burn, glitch, annoy your cat - anything can happen

to be able to use this you will have to obtain a specific beta build (bare_metal) through the RNBO beta list - if you are not already a member and are interested in taking part, pls contact us through: contact@cycling74.com

## Note

While this specific example is aimed at the Daisy Platform, the general idea is that the minimal version of the RNBO code
export is useable on various bare metal platforms, so if you represent one and are interested in testing RNBO code
out on your hardware, please contact us !

## Prerequisites

Be sure to follow these instructions to get a fully working Daisy toolchain first:

https://daisy.audio/tutorials/cpp-dev-env/#1-install-the-toolchain

please only try out this exmaple after you successfully exported a few Daisy examples on to your hardware.

## Installation

This repo does not require any specific installation - just check it out and int/update all submodules (recursively !).
Installing the Daisy toolchain should already have equipped with all the necessary software

### Bootloader

since RNBO patches can be quite large, we are using the boot loader

https://electro-smith.github.io/libDaisy/md_doc_2md_2__a7___getting-_started-_daisy-_bootloader.html

please follow the above instructions to flash the bootloader on your hardware

### Memory

In this example we move all audio sample allocations to Daisy SDRAM, based on this HowTo:

https://electro-smith.github.io/libDaisy/md_doc_2md_2__a6___getting-_started-_external-_s_d_r_a_m.html

while this seems to work fine for now, and might match quite a few use cases, this might be not the best
was to deal with memory - if you are a Daisy dev and think there are better ways to handle this, we would 
be really happy if you would reach out to us

## Export

RNBO C++ Source Code Export generated files need to go into the _export_ directory. Be aware that you need to
use the "Minimal Export" feature introduced on the bare_metal branch to generate code that works with this example.

Consider using a fixed vector size that matches the one set in the example (currently 64 samples, but feel free to 
change it to your needs) for your export.

## Usage - Command Line

before you can get started you have to build libDaisy

    cd 3rdparty/libDaisy/
    make

now go back to the repo root dir and type

    make

Now put the Daisy bootloader into *DFU mode* without cycling through the other modes by:

Press and release reset, then press and release boot button.

Notice: The Daisy Seed LED will be the “breathing” LED indicating the Daisy bootloader is waiting for a DFU connection.

    make program-dfu


## Usage Visual Studio Code

You will have noticed that there is a .vscode directory, containg a tasks and some cortext debug settings. If
installed VSCode though the above toolchain link, they might come handy:

- Open the rnbo.example.daisy folder in VS Code
- Ctrl-P and write _task_

and then you should already see the options, you will ahve to start with

    task build_libdaisy

Now put the Daisy bootloader into *DFU mode* without cycling through the other modes by:

Press and release reset, then press and release boot button.

Notice: The Daisy Seed LED will be the “breathing” LED indicating the Daisy bootloader is waiting for a DFU connection.

and then:

    task build_and_program_dfu


## MIDI

This example should advertise a MIDI port named something like: _Daisy Seed Built In_


## More Information

in general the Daisy forums are a great source of information - i found this one especially helpful:

https://forum.electro-smith.com/t/out-of-flash-memory-walkthrough-with-samples/4370
