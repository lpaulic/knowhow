# Yocto Project

## Intro

It is an open-source project for building custom Linux OS for target boards.
It is a collection of build frameworks (build systems), tools, and metadata. 
Its major components are OpenEmbedded, Poky, and Bitbake. The Yocto Project 
supports many different architectures (PowerPC, ARM, x86/64, etc.) and hardware
platforms. For more info visit [Yocto Project](https://www.yoctoproject.org/)

Fun fact: yocto is (10^-24).

The structure of a Yocto Project repository is:
- layers:
    - BSP type, 
    - Base type, 
    - Distribution type, 
    - Miscellaneous type,
    - Software type
- bitbake

This is the bare minimum. The versioning is explained in the [Release strategy](#release-strategy) 
section. There can be, often there are, multiple layers in a Yocto Project 
repository. There can also be multiple layers of the same type.
But a good practice is to have on BSP layer per Yocto Project in practice.
There are always multiple Base, Software and Miscs type layers.
There can be multiple Distro type layers in a Yocto project but that is 
haly dependent on the domand in project for which the specific Yocto 
Project repo is being developed. 

Other optional thins in a Yocto Project repository are various helper tools
in form of scripts or other binaries. Most of the scripts come from the 
openembedded-core layer. They aid the developer in working with layers,
build, test, and releases.

An example implementation of a Yocto Project is Poky.

## Components

Components used by the Yocto Project
- [OpenEmbedded](./openembedded.md)
- [Bitbake](./bitbake.md)

Components provided by the Yocto Project
- [Poky](./poky.md)
- layers:
    - meta-yocto, distro type (Poky)
    - meta-yocto-bsp, bsp type
    - etc.
- [SDKs](./sdk.md)
- tools:
    - [toaster](./toaster.md)
    - [devtool](./devtool.md)

## Release strategy

When in comes to releases in the Yocto project multiple components need to be 
taken into consideration.

The Yocto Project itself is versioned. It uses the semantic
versioning and for minor releases it has codenames associated with it. For 
example Yocto version 5.0 is also called Scarthgap.

The layers used in Yocto Projects are tightly related to the Yocto Project 
versioning. The layers can have their own versioning logic but they are based 
on a certain version of the Yocto project. It is also commong to Yocto version
names in the layer version.

Bitbake is a separate utility that is used by the Yocto project and it has its 
own release plan and scemanting versioning. Since the Bitbake is the building 
block of the Yocto project each version of Bitbake is related to a Yocto
version.

Poky reference project utilizes OpenEmbedded and Bitbake and is version 
according to the Yocto Project versions. It used to have separate versioning 
up to Poky version 23.0, Yocto Project version 3.1. 

Link to the Yocto Project release: [Yocto Releases](https://wiki.yoctoproject.org/wiki/Releases)

## Custom Yocto Project based repository

- Distribution layers should be architecture agnostic, so only userspace tools 
that are hardware agnostic should be located in distro layers
- All layers should be tight together in a spearate repository or a repo 
compatible manifest. The hardware agnostic distor is married with the hardware 
with configuration files
- Board specific layers should depend on layers for components that are used 
on the hardware (i.e.: MCU or SOME)
- when running `openembedded-core/oe-init-build-env` where `Bitbake` is not in 
the same directory as `openembedded-core` you need to specify it as a second 
argument after first argument, the build directory.
- Most common essential layers: core (openembedded-core), openembedded-layer 
(meta-openembedded/meta-oe), meta-python (meta-openembedded/meta-python)
- Yocto Embedded Linux project template:

```
yocto-project/
├── bitbake/                     # Bitbake folder used to run the bitbake build tool 
├── sources/                     # All layers used in the project, can be git submodules or local directories
│   ├── meta-stm32/
│   ├── meta-application/
│   ├── meta-openembedded/
│   ├── meta-yocto/
├── build/                       # build folder, contains build artifacts
├── conf/                        # project Yocto configuration: bblayers.conf, local.conf
├── scripts/                     # helper scripts: init, build, CI/CD configuration and scripts, etc.
├── README.md 
├── CHANGELOG.md 
├── LICENSE
└── .gitignore

```

## Links and resources

1. [Udemy - Embedded Linux with Yocto](https://www.udemy.com/course/embedded-linux-using-yocto/learn/lecture/21952330#overview)
2. [Yocto technical overview](https://www.yoctoproject.org/development/technical-overview/)
3. [Yocto Project Development Tasks Manual](https://docs.yoctoproject.org/dev-manual/index.html)
4. [Yocto Project Board Support Package Developer’s Guide](https://docs.yoctoproject.org/bsp-guide/index.html)
5. [Yocto System requirements](https://docs.yoctoproject.org/ref-manual/system-requirements.html)

