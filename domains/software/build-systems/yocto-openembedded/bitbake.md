---
layout: default
title: Bitbake
parent: Yocto OpenEmbedded
nav_order: 3
---

# Bitbake
{: .no_toc }

## Intro

Core component of the Yocto project. Performs the same functionality as Make. It is a
task scheduler that can pars Python and shell scripts. The parsed code generates and
runs tasks. A task is a set of steps, order by code's dependencies, that need to be
executed. It reads recipes and follows them by fetching them, building and
than incorporating into bootable images.

It tracks all of the tasks being processed in order to ensure completion maximizing
the use of processing resources to reduce build time.

## Metadata

Build instructions (commands and data) used to indicate what 
versions of software are used, where they are obtained from, changes
or additions to the software (patches).
The metadata in Bitbake are commands and date which are implemented through variables,
tasks and dependencies. These metadata are used to create: configuration files,
recipes, classes, includes.

## Variables

Basic elements of recipes (with classes, includes) and configuration files.
The general assignemt to variables follows this pattern:

```
VARIABLE <assignemnt-typte> ["data"|'data']
```
There are multiple assignment types:
- hard assignment `=`: sets the value to variable with out constraints;
the assignment is immediate; if multiple assignment of this type exist
the last one will be used
- soft assignment `?=`: set the value to variable only if the variable 
is not defined before this assignment at parsing time; assignment is immediate; 
if multiple assignments of this 
type exist the first one parsed will be used
- weaker default assignment `??=`: same as the soft assignment but the assignment
part is done after parsing process rather than immediately; if multiple 
assignments exists the last one parsed will be used; both hard and soft assignments
will override the weak default assignment
- immediate variable expansion assignment `:=`: same as hard assignment except that 
the expansion of the variables in the value are immediatally

Both signe and double quotes are supported. Guideline is to use double quetes
by default and use single quotes when double quotes are part of the value.
Whitespaces are taken into account in assignments. Variables assignment can
be split input multiple lines using the `\` character. Use the following format
to reduce the number of whitespaces in variable assignment:

```
VARIABLE <assingnemnt-type> "\
value1 \
value2 \
value3 \
"
```

Alongside assignment we have appending operators:
- `+=`: append value to variable with whitespace before the appending value 
- `.=`: append value to variable without whitespace

Appending operators take effect during parsing. Order of assingement and 
appending operator matters.

Alongside assignment we have prepending operators:
- `=+`: prepend value to variable with whitespace after the appending value 
- `=.`: prepend value to variable without whitespace

Prepending operators take effect during parsing. Order of assingement and 
prepending operator matters.

Instead of using appending/prepending operators you can use the Override style syntax:
- appending:

```
VARIABLE_append = " value" # Bitbake <2.0
VARIABLE:append = " value" # Bitbake >=2.0
```
- prepending:

```
VARIABLE_prepend = "value " # Bitbake <2.0
VARIABLE:prepend = "value " # Bitbake >=2.0
```

NOTE: Overriding style syntax does not insert whitespaces by default.

Guideline would be to use overriding style syntax on variables whose
scope is wider than one file.

Values can be removed from variables using the removal syntax:

```
VARIABLE_remove = "value" # Bitbake < 2.0
VARIABLE:remove = "value" # Bitbake >= 2.0
```

Advantage of the overriding style syntax is provide guarantee that it will perform 
the action regardless of the parsing order. The operators will fail if the 
assignment was not done before append/prepend.

Variable can be set in configuration files and in recipes.
Variables can be checked after the metadata has been parsed.
To read they variable values use the following commands:
- read configuration variable values:

```
bitbake -e | grep ^VARIABLE="
```
- read recipe variable values:

```
bitbake recipe -e | grep ^VARIABLE="
```

To use variable values (variable expansion) in other recipes and configuration
files use the following syntax:

```
${VARIABLE}
```

When `=` is used, variable expansion is not done immediatally rather it is 
deferred until the variable assigned to is used. Also if the variable 
used in expansion is note defined the string will be used as is.

Variables in configuration files (distro, layer, local, machine) are global.
Variables in recipe files are local to the particular recipe.

Full list of OpenEmbedded variables available here: [Yocto Variable Glossary](https://docs.yoctoproject.org/4.0.17/ref-manual/variables.html)

## Tasks

Tasks are the smallest working unit from the perspective of the Bitbake 
build engine. OpenEmbedded predefined tasks that can be 
found here: [Task List](https://docs.yoctoproject.org/ref-manual/tasks.html)

Custom tasks can be added and they are included in the build with the following
commands added in the recipe:

```
addtask do_<custom-task> after do_<task-A> before do_<task-B>
```
The `task-A` and `task-B` can be standard tasks or other custom tasks.

Some good to know information for each of the most used standard tastsk can be
found in following subsections.

### do_fetch

Order of the task in the build process: 1.

Source fetching is controlled by the `SRC_URI` variable. The `SRC_URI` must 
contain one or more location(s) to the source. Bitbake supports the following 
URL schemas:
- `git`
- `https`
- `svn`
- `ftp`
- `file`

The `SRC_URI` must contain URIs in the following syntax: 
`scheme://url;param1;param1;paramN`. The scheme can describe a local file 
(file://) or a remote location (https://, git://, etc.). Each scheme has its on
specific in the URI string, and they can be found here: [Fetching](https://docs.yoctoproject.org/bitbake/2.0/bitbake-user-manual/bitbake-user-manual-fetching.html).
By default the downloaded source is placed in the `${BUILDDIR}/downloads` 
directory but only if the source is not local.

To build an recipe run: `bitbake <recipe-base-name>`. If multiple versions 
exist Bitbake will build the latest one. A specific task can be executed by
running: `bitbake -c <task> <recipe-base-name>`. To list task for a pritcular
recipe run: `bitbake -c listtasks <recipe-base-name>`.

Recipes should be placed in a directory with the same name as the recipe. 
Relative paths should be used in when specifying local files in recipes.
Bitbake by default searches for local recipe files in the
`<recipe-directory>/files` or `<recipe-directory>/<recipe-name>`

NOTE: If patch files exist, even locally, they need to be specified in the
`SRC_URI` variable.

When fetching freom Git repository `SRCREV` needs to be specified, and S must
be set to `${WORKDIR}/git`. `SRCREV` can either be set to `${AUTOREV}` which 
represent the latest revision in the repository being fetched. The other
approach is to specify a hardcoded revision, for Git it can be a git commit 
hash. To specify a special branch add `branch=` option to the git URL in 
`SRC_URI`. To use local Git repository so builds can be verified without 
pushing upstream set the `protocol=` option to `file` instead of `https`. The
URL in the local Git case should point to the repository absolute path on your
local machine. To use private SCM repositories in builds the `protocol=` option
should be set to `ssh` and you should have a public-private SSH key pair
generated on your machine. Add the public key to the Github repository. 
To specify a tag that represents the revision use the `tag=` option in the 
SRU_URI. When the `tag=` option is used the `SRCREV` is not needed.

### do_unpack

Order of the task in the build process: 2.

All files found in the `SRC_URI` are copied to the `${BUILDDIR}/tmp/work` 
directory. Whene extractuing an archive Bitbake expects to find extracted files
in directory named `<application>-<version>`. This is controlled by the `S` 
variable. If the archive doesn't produce this directory you must specify the 
proper directory name in the `S` variable. If you are fetching with SCM 
(git or svn) you must specify the directory name in `S`. For git scheme the `S`
should be: `S=${WORKDIR}/git`

Additionally to the software license need to be known to Bitbake when building.
Both `LICENSE` and `LIC_FILES_CHKSUM` need to be specified in the recipe. The 
`LICENSE` contains a license type string that the software is using. To find
out which license is used in software check for a `COPYING`, or `LICENSE` files
or look into the `README` or at the top of source code file. For standard 
licenses use name strings defined in `meta/files/common-licenses/`. The 
`LIC_FILES_CHKSUM` needs to hold a URI path to the file containing the license 
with the checksum option, i,e `md5=xxx`. This variable is used to verify if the 
license file has changed.

### do_patch

Order of the task in the build process: 3.

After fetching the software source code any files in the `SRC_URI` that end 
with `.patch` or `.diff` suffixes are treated as patch files. This stage 
automatically applies the patch files. By default the Bitbake uses the `-p1`
option when applying patches. If more directory levels need to be stripped off
use the `striplevel` option in the `SRC_URI` entry for the patch.

When adding patches to through a `.bbappend` start the numbering from 
`9xxx-patch-name.patch` so we can guarantee that they will be applied last. But
first check if there are other `.bbappend` files.

### do_prepare_recipe_sysroot

Order of the task in the build process: 4.

Stage where the recipe's sysroot is prepared before running build stages. 
Setus up `recipe-sysroot` and `recipe-sysroot-native`.

### do_configure

Order of the task in the build process: 5.

Stage where build time configuration is set for the software before compilation.
If you are not using the common build tools (CMake, Make, Autotools) and 
inherit their classes a `do_configure` tasks must be specified.

### do_compile

Order of the task in the build process: 6.

Bitbake takse all the variable settings and sources from the previous stages
and compiles the software.

### do_install

Order of the task in the build process: 7.

After the software is compiled the output files, the whole hierarchy that 
mirrors the location as on the target device, is copied to a staging directory.
Utilize the `install` command provided by Bitbake. It combines the `mkdir`, 
`cp`, `chmod` and `chown` commands.

### do_populate_sysroot

Order of the task in the build process: 8.

Copies a subset of files installed by the `do_install` into appropriate sysroot.
The files are copied to the recipe's `WORKDIR/sysroot-destdir` which is the 
shared sysroot directory.

### do_package

Splits the files produced by the recipe into logical components. Logical 
components are typically: debug symbols, Documentation development files, etc. 
Splitting happens because embedded systems do not have the same amount of 
memory resources as general purpose machines. So dockuemtation, development 
resources, etc. are split into different packages which are not installed by 
default. The splitting is controlled via `FILES` and `PACKAGES` variables.

Since the bitbake configuration provides the default groupings for the logica 
components, setting `FILES` and `PACKAGES` do not need to be set unless your 
recipe is installing artifacts in non-standard locations.

To install split packages in the image they need to be added to the 
`IMAGE_INSTALL` variable. For example to  add debug package: 
`IMAGE_INSTALL += "package-dbg"`.

If the same artifact is specified to multiple packages it will end up inside
the package that is specified first in the `PACKAGES` variable. An artifact 
can only be provided by one package for a single recipe.

Custom packages can be created by adding `${PN}-<custom>` `PACKAGES`, 
and adding artifacts for the custom package.

## Recipe files

Set of instructions on how to build a package. 
How to build it, how to configure it, how to depoloy it.
Extension used: `.bb`, `.bbappedn` (recipe append files)

Recipe name file format must follow the following rules:
- File name format: `<base-name>_<version>.bb`
- The `<version>` part should follow the schematic versioning rules
- Use lowercase characters and avoid reserved suffixes: 
`-native`, `-cross`, `-initial`, `-dev`

Recipes are build using the Bitbake build tool. Bitbake parses the recipes and
generates a list of tasks that it executes to perform the build.

The most imporatnt Bitbake tasks:
- `do_fetch`: fetch the software source
- `do_unpack`: extracts the source into a working directory
- `do_patch`: find patch files and apply them to the source
- `do_configure`: configures the source depending on the build tool used
- `do_compile`: compiles the source
- `do_install`: copies the compilation directories to a holding (staging)
directory
- `do_package`: analyzes the staging directory and splits into subsets based on
packages and files
- list of all tasks: [Bitbake Tasks](https://docs.yoctoproject.org/dev/ref-manual/tasks.html?highlight=tasks)

In general user needs to specify only:
- `do_configure`
- `do_compile`
- `do_install`

Predefine tasks depending on the build tools used already exist: 
`Autotools`, `Cmake`, `QMake`, etc.

Custom tasks can be created and define the order in the task list. All recipes
automatically inherit the `meta/classes-global/base.bbclass` which define basic
tasks, some run something basic some are empty.

Logging in recipes is supported for both Python and Shell langues in the recipe.
In Python recipe code logging is done using:
- `bb.fatal`: highest priority, execution will be terminated, logs will appear 
on stdout as well
- `bb.error`: logs will appear on stdout as well but execution will not
terminate
- `bb.warn`: logs will appear on stdout as well
- `bb.note`: not to user
- `bb.plain`: output a message
- `bb.debug`: debug messages, to show on stdout pass `-D[D[D]]` flag 
to bitbake

The logs, when using python, endup in: `TMPDIR/tmp/log/cooker/<machine>`

In shell scripts similar syntax is used:
- `bbfatal`: highest priority, execution will be terminated, logs will appear
on stdout as well
- `bberror`: logs will appear on stdout as well but execution will not 
terminate
- `bbwarn`: logs will appear on stdout as well
- `bbnote`: logs will appear on stdout as well, note to user
- `bbplain`: logs will appear on stdout as well, output a message
- `bbdebug`: debug messages, to show on stdout pass `-D[D[D]]` flag to 
bitbake

The logs, when using shell, end up in: 
`TMPDIR/tmp/work/<arch>/<recipe-name>/<software-version>/temp`

Attributes are metadata used to set specific for an variable or a task. Syntax 
is: `variable[attribute] = "value"`. One of the available attributes for tasks 
is: `task_name[noexec]`. If set to "1" will tell the OE build system not to
execute the particular task.

### Image recipes

Top level recipe, it has a description, a license, and inherits the core-image 
class. It is used alongside the machine definition. Machine describes the 
hardware used and its capabilities. Image is architecture agnostic and defines 
how the root filesystem is built, with what packages. Several images are 
provided in Poky. Command to check available image recipes: 
`ls meta*/recipes*/images/*.bb`

There are two ways to create an image recipe:
- From scratch
- Using an existing recipe (preferable)

When creating images package groups are used. A package group is a set of 
packages that can be included in any image. Package groups contain a set of
packages. Using the package group name in `IMAGE_INSTALL` variable installs 
all the packages defined by the package group into the root file system of the
target image. Many predefined package groups exist. They are located in 
subdirectories named `packagegropus`. Package groups are recipes that start
with `packagegroup-`.

Creating image recipe from scratch:
1. Create `image` directory in the right `recipe` category directory
2. Inherit the `core-image` bbclass, which will by default have everything 
necessary for building an image. `core-image` inherits `image`.
3. Extend the `IMAGE_INSTALL` variable with desired package names
4. Set other variables: `SUMMARY`, `DESCRIPTION`, `IMAGE_ROOTFS_SIZE`

Create image by reusing existing image:
1. Create `image` directory in the right `recipe` category directory
2. Require the base image that we want to reuse: 
`require <path-to-image-recipe>`
3. Make changes to variables by using overwriting style syntax to remove what 
isn't needed and add what is.

What can also be done is to create an include file that has the common parts 
for all images and that that include is required by all image recipes with 
specific changes.

Image can be customized by using the `IMAGE_FEATURES` and 
`EXTRA_IMAGE_FEATURES`. These variables provide a means to enable high-level 
features, for example: empty password for root, debug image, special packages, 
x11, splash, ssh-server, etc. The difference between `IMAGE_FEATURES` and 
`EXTRA_IMAGE_FEATURES` is in the best pracitces where they are used. 
`IMAGE_FEATURES` should be used only in image recipes. `EXTRA_IMAGE_FEATURES`
should be used in the local configuration file.

The behaviour of the image feature is defined in the 
`meta/classes-recipe/core-image.bbclass` class file. In this file available 
image features are listed. It can be seen that the image features ar basically 
keys that map to package groups that hold all the packages necessary for a 
feature. Based on this Bibake will add this package groups to the image.

There are other useful image variables:
- `IMAGE_LINGUAS`: list of locales to install into the image during the image
construction phase
- `IMAGE_FSTYPES`: determines the rootfile system image type. If more formats 
are specified an image for each type will be generated. Image format 
instruction can be found here: `meta/classes-recipe/image_types.bbclass`. 
Custom image types can  be created, the `image_type.bbclass` must be inherited.
Reference `sdcard_image-rpi.bbclass`.
- `IMAGE_NAME`: specify the name to use when generating the image file. Only 
the name is specified the extension is appended by the build system.

Image manifest file lists all the packages that make up the image. The file 
contains the following line-per-packeg format:

```
packagename packagearch version
```

The `image.bbclass` defines a default manifest file name.

Image recipes should be written independently from the distribution 
configuration. Order of parsing must be taken into account, image recipe is 
parsed after distribution configuration and can override distribution settings.
Guideline should be that variables overwritten in the image recipe should use 
weak assignment.

### Static library recipes

Most important aspect when writing a library recipes is the location of the 
files and packages that include them. Location of files:
- *.a -> ${libdir}
- *.h -> ${indcludedir}

Package that will include the artifacts are: `${PN}-staticdev` and `${PN}-dev`.

### Dynamic library recipes

Shared libraries (position independent code - PIC) follow certain naming 
convention:
- Linker name (e.g.: libexample.so)
    - linker name follow this template `lib<library-name>.so`
    - name requested by the linker when another code is linked with the shared 
    library (-l flag)
- Soname (e.g.: libexample.so.1.2)
    - soname follows this template `lib<library-name>.so.<major-version-number>`
    - library name that includes important interface changes
    - written in the `*.so` elf file format
    - the change is depicted in the number version after the `.so` suffix
- Real name (e.g.: libexample.so.1.2.3)
    - real name follow this template 
    `lib<library-name>.so.<major-version-number>.<minor-version-number>.<patch-version-number>`
    - library name that includes the full version

Library using the real name is a file and other two are symbolic links. Soname
is symbolic link to real name file, and linker name is a symbolic link to 
soname file.

Most important aspect when writing a library recipes is the location of the 
files and  packages that include them.
Location of files:
- *.so* -> ${libdir}
- *.h -> ${indcludedir}

Package that will include the artifacts are: ${PN} and ${PN}-dev
Linker an real name end up in the ${PN}, while the rest ends up in ${PN}-dev

It is common to have libraries that are not version (unfortunately). BitBake 
will report QA issues when dynamic library only has soname. In those instances 
to ensure that the dynamic library is present in the image when adding only the
`${PN}` additional work in the recipe is needed. The variable `SOLIBS` needs to 
be set to `SOLIBS=".so"` and `FILES_SOLIBSDEV` needs to be set to 
`FILES_SOLIBSDEV=""`. This will change installation behavior just for the 
package making this changes. In unversioned dynamic libraries the linker name 
library is not a symbolic link.

### Recipe search paths

By default OE build system searches the directories:
- `<recipe-directory-path/files/`
- `<recipe-directory-path/<recipe-name>/`
- `<recipe-directory-path/<recipe-name>-<version>/`

This enables us to not write absolute paths in `SRC_URI` when using the
`file://` schema. The paths where bitbake searches for are defined in 
`FILESPATH`, `FILESEXTRAPATH`, and  `FILESOVERRIDES`.
Files path definition ca be found in `meta/classes/base.class`. Values in these
variables are colon (:) separated and searched left-to-right.

If there is a need for additional file path extend the `FILESEXTRAPATH`. Never 
hand-edit the  `FILESPATH`. The `FILESPATH` is automatically extended with 
`FILESEXTRAPATH` and `FILESOVERRIDES`.

The `FILESOVERRIDES` enables us to have separate files for specific machine 
types or distros or other conditional values. The content of this files changes
the path searched. By default it is extended by the distor and machine values.
The when creating recipe files machine/distor specific files should be put in 
i.e.: `files/<machine>/*`. The `SRC_URI` does not have to be changed and that 
is the beauty.

The `FILESEXTRAPATH` extends the search path for the OE build system. 
The syntax is usually like this:

```
FILESEXTRAPATH:prepend = "${THISDIR}:"
FILESEXTRAPATH:prepend = "${THISDIR}/${PN}:"
```

Following best practices the `FILESEXTRAPATH` should be used in the 
`.bbappedn` files.

### Recipe providers

Various aliases by which the recipe can be referenced from bitbake.
BitBake has two namespaces:
- recipe name (build-time target)
- package names (runtime targets)

BitBake CLI takes recipe names and input arguments and not package names.
Package names are used on the target and in some variables in bitbake 
(e.g.: RDEPENDS, `IMAGE_INSTALL`, `PACKAGES`, etc.)

Virtual targets are are supported in BitBake and they are a alias name 
corresponding to a specific functionality (i.e.: kernel, compiler, bootloader).
In general recipes the provide a specific functionality add the virtual target 
name to the `PROVIDES` variable. Virtual targets, by convention, have the 
following name template: `virtual/<functionalityname>`. Slash is part of the
name string, it has  no special meaning. It is advised to use the 
`virtual/<functionalityname>` for recipes that provide them because it provides
apstraction so specific machines and version don't need to specified.

When multiple recipes provide the same functionality priority is given by using
the following command: 
`PREFERRED_PROVIDER_virtual/linux = "<desired-recipename>"`

### Recipe preferences

Used when there are multiple recipes with the same name but differ in version.
In that case `PREFERRED_VERSION_${PN}` should be used. Version syntax supported:
- specific version in sematci versioning syntax
- using `%` wildcard

### Recipe compatibility

A recipe is considered incompatible with the currently configured machine when 
either or both `COMPATIBLE_HOST`and `COMPATIBLE_MACHINE` specify compatibility 
with a machine other than the current machine or host.

It is possible to enamble only certain arcihtectures by using:

```
CONFIGURE_MACHINE = "(-)" # disallow all architectures
CONFIGURE_MACHINE_x86 = "(.*)" # allow x86
CONFIGURE_MACHINE_armv6 = "(.*)" # allow armv6
```
Or allow all but turon off specific:

```
COMPATIBLE_MACHINE_armv4 = "(!.*amrv4).*"
```

## Extended recipe

A good practice and it is highly advised: 
*DO NOT MODIFY RECIPES IN OTHER LAYERS*.
But sometimes it is useful or even required to modify some recipes.

The basic, not advised approach, is to copy the recip to custom layer and make
modifications there. The better approach is to extend the existing recipe in 
the layer by extednig it using `.bbappend` files in you custom layer. Downsides
of this approach is that the changes must be added manually to the recipe copy 
when the original changes with time.

The `.bbappend` files are a form of recipes that appends metadata to the 
original `.bb` recipe. How it works is  that the OE build system 'appends` the
content of the append recipe to the original recipe. The OE build system 
matches the recipe name with the recipe append name. The recipe appends should 
be in the custom layer, where the  holding directory of the recipe append file 
is the same as the original recipe file. So the rules are:
- root file must be the same between the recipe and the recipe append file,
including version if specified
- recipe file must exists somewhere in the build environment

Layer priorities affect the recipe overriding as well as applying append files. 
The recipe file from a layer with higher value will take precedence. The append
file in the layer with the highest priority will be applied last.

NOTE: Also the recipe append files are merged with the recipe files. It is
important to avoid name duplications.

BitBake offers an command to check all appends for all recipes: 
`bitbake-layers show-appends`. It can be combined with grep command to filter 
out appends only for specific recipe.

## Configuration files

File which holds:
- global definition of variables
- user defined variables
- hardware configuration information

They tell the build system what to build and put into the image to support a 
particular platform. Extension used: `.conf`.
Types of configuration files:
- machine configuration options
- distribution configuration options
- compiler tuning options
- general common tuning options
- user configuration options (`local.conf`)

### Machine configuration file

Rules of thumb when writing machine configuration files:
1. Find machine configurations of the closest related chip, soc, some for chip that is being worked on.
2. The common include files are for versions, default providers and tune settings.
3. Set variables that are vendor specific and automatically set variables in point 4.
4. Ensure that these variables are set in the machine config:
    - MACHINE_ARCH
    - MACHINE_FEATURES
    - MACHINE_EXTRA_RRECOMMENDS
    - MACHINE_ESSENTIAL_EXTRA_RRECOMMENDS
    - TUNE_FEATURES
    - DEFAULT_TUNE
    - PREFERRED_PROVIDER_virtual/<functionality>
    - PREFERRED_VERSION_<recipe>
    - IMAGE_FSTYPES
    - EXTRA_IMAGEDEPENDS
    - IMAGE_BOOT_FILES
    - KERNEL_IMAGETYPE
    - KERNEL_DEVICETREE
    - KERNEL_MODULE_AUTOLOAD
    - SERIAL_CONSOLE
    - BOOTLOADER
    - UBOOT_MACHINE
    - UBOOT_CONFIG
5. Assignment in machine configuration should be soft and weaker default. 

### Distribution configuratio file

## Class files

Abstract common functionality and share them between multiple recipes. By 
functionality it is often referred to functions, tasks, etc., that are used by 
multiple recipes. Extension is: `.bbclass`.

## Include files

TODO:

## Packages

A package is a binary file with name *.rpm, *.deb, or *.ipkg. A single recipe 
produces many packages. All  packages that a recipe generated are listed in the
variable `PACKAGES`.

## Layers

Layers are metadata defined by the OpenEmbedded Project but since the layer 
usage is mostly  done in Bitbake we will explain it here.
Layers enable us to:
- Store recipes for custom software projects
- Create custom images
- Consolitade patches/modifications to 3rdparty recipes
- Add custom kernel
- Add custom machine

Depending on the layer content, add the content:
- if layer is adding support for a machine, add the machine configuration in
`conf/machine/<machine-name>.conf`
- if layer is adding distro policy, add the distro configuration in
`conf/distro/<distor-name>.conf`
- if layer introduces new recipes, put the recipes you need in `recipes-*` 
subdirectories of the layer directory
- layer configuration in `conf/layer.conf`

Recipe directories inside layers are categoriezed. REcipes should go in the 
right directory. This is the hardest part when writing a recipe, the recipe 
category :). Good practice is to check the Yocto compatible layers and check 
where did they put the similar recipe. Goes for append files as well they 
should have the same path as the recipe they are modifying.

Each layer has a priority which is used by bitbake when deciding which layer 
takes precedence if there are  recipe files with the same name in multiple 
recipes. Higher number represents higher priority value.

There are two way to create layers:
- Manually
- Using predefined bitbake script

Manually creating layers include the following steps:
1. Create a directory for the layer following the naming convention for layers.
2. Create a `conf/layer.conf` file in the layer root directory. You can copy 
the `meta-oe` layer skeleton configuration and change value accordingly.
3. Update `BBLAYERS` variable with then new layer

Using bitbake script:
1. Run command: 
`bitbake-layers create-layer <path-to-layer-parent-dir>/<layer-dir-name>`.
Default layer priority is 6.
2. OPTIONAL: Use additional flags for set priority or add recipes.
3. Add layer to the build system: 
`bitbake-layers add-layer <path-to-layer-parent-dir>/<layer-dir-name>`

The layer is configured through its `layer.conf` file. The `layer.conf` file 
does the following:
- appending the current layer directory to `BBPATH` variable with `:` 
as delimiter
- appending the recipe and recipe append file paths to `BBFILES` variable
- setting the layer priority to `BBFILE_PRIORITY_<layer-name> = "<priority>"`
- list of yocto branch version that the layer is compatible with 
`LAYERSERIES_COMPAT_<layer-name> = "<list-of-branch-names>"`
- list of dependency layers:
`LAYERDEPENDS_<layer-name> = "<list-of-depencency-layers>"`
- layer version to indicate major compatibility changes 
`LAYERVERSION_<layer-name> = "<major-version>"`

Yocto provides a script to check custom layer compatibility with the
Yocto project:

```
source oe-init-build-env
yocto-check-layer <custaom-layer-directory-path>
```
This is only crucial if the layer must pass the Yocto compatibilyt program.

If the configuration file is not present when build
starts the OpenEmbedded build system creates it from `bblayers.conf.sample` 
when the oe-init-build-env-script is sourced.
Command to list used layers: `bitbake-layers show-layers`.

## Dependencies

Software packages most often need other software packages to build or run, they 
are called dependencies. There are two types of dependencies:
- build-time dependencies: packages need during building of a software package
- runtime dependencies: packages needed on the target when a software package 
is being run

To show task dependencies invoke bitbake with: `bitbake -g <recipe-name>`. This
generates two files:
- pn-buildlist: list of recipes/targets involved in building a recipe. 
"Involved" means at least one task.
- task-depends.dot: DOT format file depicting the task dependency.

Additionally `-u taskexp` can be specified after the `-g` flag to display 
dependencies in and GUI explorer.

## Sharing files between recipes

Files between recipes are sherd using `sysroot`. One `sysroot` exists per 
`MACHINE` and it is split into:
- sysroot for the trarget machine
- sysroot for the build host

Subset of files installed into standard locations are automatically copied into 
the `sysroot`.

## Development shell

Shell which is running in the same context as the BitBake task engine. This 
shell is available as a command for every recipe: 
`bitbake -c devshell <recip-name>`. All the environment variables necessary for
BitBake and the particular recipe are available. This enables user to do 
experiments and check their work to see if the recipe changes are working. 
The `do_devshell` task is executed after the `do_prepare_recipe_sysroot`.

When building in the development shell make sure you use the environment 
variables as defined in the recipes. Reason why is because the variables have 
additional flags set that are necessary for the command to be executed
successfully.

NOTE: any changes made in the devshell are not persistent between builds. 
The changes must be persisted in some  way so they are not lost. A good way is 
to use patch files. If the repository doesn't use Git than a git repository 
must be created. Be aware that if the git repository, or patch files are 
created in the build folder it will be deleted if cleanall task is run.

## Building basics

There are two types of build:
- Clean build: 
    - build of software from scratch
    - advantage is that everything is build from zero and there is no 
    possibility of stale data
    - building from scratch takes much longer because everything is 
    rebuilt, including packages that do not necessarily need to be 
    rebuilt
- Incremental build:
    - identify what does not to be rebuild 
    - build only things that have been modified from the last successful 
    build
    - takes considerably less than clean build

Creating and initializing a new build performs a clean build.

### Incremental build

Supported by the Yocto project. Utilizes the shared state cache mechanism to 
build only the strictly necessary components for a given change. For this to 
work, the build system calculates a checksum of a given input data to a task.
If the input data changes the task needs to be rebuilt. If all input data stay 
the same build artifacts from sstate-cache will be copied to the destination. 
Tasks that a skipped task depended on will bi skipped.

#### Sstate-cache

Build performance comparison on a machine that has 40+ cores and more than 
64GB of RAM, building minimal image:
- Build with no sstate-chache or clean build: ~1.5 h
    - Parser recipes, execute all tasks
- Re-build with no changes: 10s
    - Check all hashsums and conclude there is nothing to do. Parsing of recipe
    is cached.
- Removing '<build-dir>/tmp/' directory, which holds build output data: ~1.5 min
    - Restore minimum necessary build artifacts from sstate-cache, 
    build image, etc.

To determine if a task needs to be re-run BitBake uses:
- checksums (or signatures)
    - unique signature of a task's input: configuration, recipe, files
    - terms used by Yocto project: task hash, signature, checksum
    - calculated on per-task basis to minimize rebuild
    - checksums of tasks are calculated by calculating:
        - hash of the task script
        - hash of all the dependencies (files, configuration, other tasks)
    - if any input of the task change, the hash will change
    - signatures are located in the `STAMPS_DIR`
        - this directory is used by BitBake to store accounting info 
        (what tasks have been run, what did the task do)
        - the directory structure is divided by architecture, package name and
        version
        - files in the `STAMS_DIR` are empty, because only the file name and 
        timestamps are important
        - the file name format: `$STAMP.<taskname>.<checksum>`
        - the signature data files for older version of tasks are persisted
    - stamp files are used to determine if a task needs to be rerun, only if 
    the file doesn't exist the task is run, sinche the stamp file name contains
    the checksum that is when the checksums are compared
- setscene
    - process of skipping tasks if prebuild objects are available and handling 
    the build using the prebuild artifacts
    - this enables BitBake to not build from scratch every time
    - provide a way to represent if the object is compatible with the requested 
    work being done
    - setscene works in the following way:
        - before building anything, BitBake asks whether cached information is 
        available for any of the targets and intermediate targets being built
            - BitBake first calls the `BB_HASHCHECK_FUNCTION` function with a
            list of tasks and corresponding hashes it wants to build
            - the `BB_HASHCHECK_FUNCTION` is designed to be fast and returns 
            the list of tasks, based on some logic, for which it can obtain 
            artifacts
            - BitBake runs setscene version for each task returned by 
            `BB_HASHCHECK_FUNCTION`
            - after all the setscene tasks have executed continue to next phase
        - if cached information is available, BitBake uses that information
        instead of running the main task
            - run the build for tasks that do not have available pre-build 
            artifacts
    - *some* tasks have `do_<taskname>_setscene` variant which skips the 
    buildng part that the main task does and only copies the set of files into
    specific locations needed
    - The OE build system has knowledge of the relationships between these and
    onther tasks
        
The signature of a task can be checked with: 
`bitbake-dumpsign -t <recipename> <taskname>`
Above command returns the signature data in readable format that allows to 
examine the input data used when the signature was generated. Signature data 
can be generated with: `bitbake -S none <recipename>`. Needs to be run if input
files to a task have been changed. 
The command `bitbake-diffsigs -t <recipename> <taskname>` can be run to compare 
signature files for to different invocations of the same task.

## Offline build

Yocto provides this feature and it is useful when internect connection is and
issue (non-existent or unstable).

For offline build to work a "snapshot" of the upstream sources must be created
and placed in a download directory to which the `DL_DIR` variable will 
point to. Once the download directory is ready it can be used at any time for 
any machine to replicate a build.

Steps to populate the downloads directory:
1. Start with an empty DL_DIR
    - remove files in the existing DL_DIR
    - create a new download directory and point the DL_DIR to it
2. Edit the `local.conf` as follows:

```
DL_DIR = "<path-to-download-dir>"
BB_GENERATE_MIRROR_TARBALS = "1"
```
The `BB_GENERATE_MIRROR_TARBALS` will instruct BitBake that during fetch stage
tar archives are generated from the gathered source files and stored in the DL_DIR

3. Populate the Downloads directory without Building

```
bitbake target --runonly=fetch
```
4. OPTIONAL: Remove any SCM subdirectories from the downloads directory

Now the downloads directory contains the "snapshot" of the required 
repositories.

Downside of the offline build is that it does not work for the recipes that 
attempt to download the latest version by using `SRCREV=${AUTOREV}`. Because 
when `AUTOREV` is used in the recipe the build system access the network by 
design. But typically recipes that reside in the public repositories do not
use `AUTOREV`.

An additional variable the is set in the local configuration is the 
`BB_NO_NETWORK`. 

## Links and resources

1. [Bitbake repository](https://github.com/openembedded/bitbake)
