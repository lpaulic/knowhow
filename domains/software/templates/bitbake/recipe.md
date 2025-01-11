Generic bitbake recipe template:

```
# Metadata section
SUMMARY = "Short description of the recipe"
LICENSE = "License type"
LIC_FILES_CHKSUM = "File checksum for license verification"
HOMEPAGE = "URL for project homepage"
PROVIDES = "my-package"
S = "${WORKDIR}/"
B = "${WORKDIR}/build"

# Dependency section
DEPENDS = "dependency1 dependency2"
RDEPENDS = "rdependency1"

# Source and Patch URLs
FILESEXTRAPATH:prepend = "${THISDIR}/${PN}:"
SRC_URI = "git://example.com/project.git;branch=master"

# Compile and Install Configuration
EXTRA_OEMAKE = "flags"
# EXTRA_OECMAKE = "flags"

# Tasks (ordred by their execution)
# Set task order right below the new task

# Package groups
PACKAGEGROUPS = "group1 group2"

# Other configurations
# Additional configuration options, overrides, or customizations 
# specific to the recipe may be included in this section.
inherit autotools pkgconfig
```
