# OpenEmbedded Project

## What is it?

Provides cross-compile environments that are the core building block that 
together with Yocto provide the mean to create custom Linux distributions.
For more info visit: [OpenEmbedded Project](https://www.openembedded.org/wiki/Main_Page).

Contains comprehensive set of Yocto metadata for wide variety of architectures,
features and applications.

Yocto Project on the other hand provides tools and BSP, along side metadata for
core set of architecture and specific boards.

OpenEmbedded's metadata is the foundation for other custom distors. The layer 
often contains textual files that show examplatory implementations, they are 
have `skeleton` in their name. They can be used as reference or starting point.

The `openembedded-core` (aka.: `oe-core`) is the shared collection of metadata
between Yocto Project and OpenEmbedded Project. The layer name is: `meta`.

Every Yocto Project has this layer. Most of the recipe append files extend a 
recipe from this layer.

## Components

Components provided by The OpenEmbedded Project:
- Layer structure
- OpenEmbedded Core layer

The Bitbake was initially developed and maintained by OpenEmbedded Project 
but was later, from 2005, was sepparated and became a standalone project.
Reason for the split:
1. Modularity: To make BitBake a more generic build tool that could support 
other projects beyond OpenEmbedded.
2. Maintainability: Decoupling allowed independent development of BitBake 
and OpenEmbedded.
3. Flexibility: Encouraged the adoption of BitBake by other projects, including 
the Yocto Project.

## Layers 

Concpet originating from OpenEmbedded project.It is a cllection of related 
recipes. Inside a layer recipes are divided into directories depending on the
type of the recipe. Convention of the recipe directories (component):
- recipe-bsp
- recipe-connectivity
- recipe-kernel
- recipe-support
- recipe-multimedia
- etc.

The description of this group can be found here openembedded-core layer:
[openembedded-core](https://git.openembedded.org/openembedded-core/tree/meta/recipes.txt)

Naming convention: `meta-<layername>`.

Layers enable us to isolate metadata according to functionality. For example 
layer for BSP, GUI, application, middleware, distribution configuration. 
This approach enbles us to easliy add bigger sets of metadata or replace other
sets of metadata. Layers stack on top of one another, the order is specified in
the a configuration file via priorities.


Where to find layers: [Index](https://layers.openembedded.org/layerindex/branch/master/layers/).
Where to find Yocto compatible layers: [Index](https://www.yoctoproject.org/development/yocto-project-compatible-layers/).

The content of the layer is organized in the following way 
(origin: [recipes.txt](https://github.com/openembedded/openembedded-core/blob/master/meta/recipes.txt))
```
recipes-bsp          - Anything with links to specific hardware or hardware configuration information
recipes-connectivity - Libraries and applications related to communication with other devices 
recipes-core         - What's needed to build a basic working Linux image including commonly used dependencies
recipes-devtools     - Tools primarily used by the build system (but can also be used on targets)
recipes-extended     - Applications which whilst not essential add features compared to the alternatives in
                       core. May be needed for full tool functionality.
recipes-gnome        - All things related to the GTK+ application framework
recipes-graphics     - X and other graphically related system libraries  
recipes-kernel       - The kernel and generic applications/libraries with strong kernel dependencies
recipes-multimedia   - Codecs and support utilities for audio, images and video
recipes-rt           - Provides package and image recipes for using and testing the PREEMPT_RT kernel
recipes-sato         - The Sato demo/reference UI/UX, its associated apps and configuration 
recipes-support      - Recipes used by other recipes but that are not directly included in images
```

More on layer usage in Bitbake can be found: [here](./bitbake.md#layers)

### Distribution

TODO: define

### Machine

TODO: define

## Layer index

- [OpenEmbedded Layer Index](https://layers.openembedded.org/layerindex/branch/master/layers/)

The above page is a great reference to find layers that can be used in a Yocto 
Project build. This is the first place a developer should look for a layer when 
developing a Yocto Project. When a layer is fully compatible with the Yocto 
Project guidelines and certified it has  a little `Yocto Project compatible` 
badge next to it.

Not all possible layers will be located on this index, so the next searching 
place is your preferred search engine. Most likely you will find them on a SCM 
repository (i.e. [Github](https://github.com/search?q=bitbake+language%3ABitBake&type=repositories&l=BitBake))

The layer index is also a good reference when designing a layer. You can search 
layers based on type: BSP, Distribution, Base, etc. This is the best way to 
learn what is the De Facto standard when creating a specific type of layer. 
By that I meand which recipes got to which type of layer. This knowledge falls 
into the category of 'the art of development' and separates beginers 
from experts. 
