---
layout: default
title: Image Specification 
parent: Open Container Initiative 
nav_order: 2
---

# OCI Image Format Specification
{: .no_toc }

## Overview
- OCI image format is composed by metadata and dependencies that when unpacked make up the runnable filesystem
- one of the packages of the image format are archives (.tar, .tar.gz, ...)
- one of the formats of the metadata is JSON
- main components of the image format
    - OCI Image Media Types
    - Image Manifest
    - Image Index
    - Image Layout
    - Filesystem Layer
    - Image Configuration
    - Conversion
    - Descriptor

## OCI Image Media Types
- OCI defines [MIME types](https://www.iana.org/assignments/media-types/media-types.xhtml) that are used in HTTP communication
to encode an transfer artefacts
- the following MIME types are supported
    - Image manifest (from v0.1.0):
        - formally known as:
            - (v0.1.0-v1.0.0): Image manifes format
        - `application/vnd.oci.image.manifest.v1+json`
        - backwards compatible with `application/vnd.docker.distribution.manifest.v2+json`

    - "Layer", as a tar archive compressed with gzip (from v0.1.0):
        - formally known as:
            - (v0.1.0-v1.0.0): "Layer", as a gzipped tar archive
        - (from v0.1.0, deprecated in v0.5.0) `application/vnd.oci.image.serialization.rootfs.tar.gzip`
        - (from v0.5.0) `application/vnd.oci.image.layer.v1.tar+gzip`
        - backwards compatible with `application/vnd.docker.image.rootfs.diff.tar.gzip`

    - Image config (from v0.1.0):
        - formally known as:
            - (v0.1.0-v1.0.0) Container config JSON
        - (from v0.1.0, deprecated in v0.5.0) `application/vnd.oci.image.serialization.config.v1+json`
        - (from v0.5.0) `application/vnd.oci.image.config.v1+json`
        - backwards compatible with `application/vnd.docker.container.image.v1+json`

    - Combined image JSON and filesystem changesets (from v0.1.0, deprecated in v0.3.0):
        - `application/vnd.oci.image.serialization.combined.v1+json`

    - Content Descriptor (from v0.3.0):
        - `application/vnd.oci.descriptor.v1+json`

    - OCI Layout (from v1.0.0):
        - `application/vnd.oci.layout.header.v1+json`

    - Image Index (from v1.0.0):
        - formally known as:
            - (v0.1.0-v1.0.0) Manifest list
        - (from v0.1.0, deprecated in v1.0.0) `application/vnd.oci.image.manifest.list.v1+json`
        - (from v1.0.0) `application/vnd.oci.image.index.v1+json`
        - backwards compatible with `application/vnd.docker.distribution.manifest.list.v2+json`

    - "Layer", as a tar archive (from v1.0.0):
        - `application/vnd.oci.image.layer.v1.tar`

    - "Layer", as a tar archive with distribution restrictions (from v1.0.0):
        - `application/vnd.oci.image.layer.nondistributable.v1.tar`

    - "Layer", as a tar archive with distribution restrictions compressed with gzip (from v1.0.0):
        - `application/vnd.oci.image.layer.nondistributable.v1.tar+gzip`

## Image Manifest
- three main goals of this specification
    - content-addressable images
        - image configuration can be hashed to generate an unique ID for the image and components
    - allow multi-architecture images
        - image indexes ("fat-manifest") that contain image manifests for platform-specific versions of a image
    - translatable into OCI Runtime Specification
- provides a configuration and set of layers for a single container image for a specific architecture and operating system
- supported format
    - JSON (from v0.1.0)

## Image Index
- contains information about a set of images that can span a variety of architectures and operating systems
- higher-level manifest, points to a specific manifest for one or more platforms
- optional for image providers
- image consumers should be able to process it
- supported format
    - JSON (from v0.1.0)

## Image Layout
- directory structure layout for OCI content-addressable blobs and location-addressable references (refs)
- this layout may be used in variety of transport mechanisms:
    - archive formats: tar, zip, ...
    - shared filesystem environments: nfs, ...
    - network file fetching: http, ftp, rsync, ...
- oci runtime bundle can be created by image layout and a reference:
    - following the ref to find a image manifest (possibly via an image index)
    - applying the file system layers in specified order
    - converting the image configuration into a oci runtime configuration (config.json)
- the structure of a image layout
    - `blobs` - directory
    - `oci-layout` - file
    - `index.json` - file


### Blobs directory
- contains content-addressable blobs
- directory MUST exist, MAY be empty
- blob has no schema and should be considered opaque (black box)
- directory structure looks as follows `blobs/<alg>/<encoded>`
- the content of `blobs/<alg>/<encoded>`  MUST match the digest `<alg>:<encoded>` (format for referencing blobs)
    - the `<alg>` directory and `<encoded>` file uniquely identify the hashing algorithm
    and the `<alg>` hash of the content referenced by the `<encoded>` file
- the character set of the entry name of `<alg>` and `<encoded>` must respect the grammar defined in
[Image Descriptor](https://github.com/opencontainers/image-spec/blob/v1.0.0/descriptor.md)
- `blobs` directory MAY contain blobs that are not referenced by any of the refs in `index.json` file
- `blobs` directory MAY be missing referenced blobs, in which case the missing blobs SHOULD be fulfilled by an external blob store

### Oci-layout file
- MUST exist
- MUST be a JSON object
- MUST contain an `imageLayoutVersion` field
    - specifies which version of the OCI Image Format specification is in use by this image layout
- MAY include additional fields
- defines the following `mediaTypes`:
    - `application/vnd.oci.layout.header.v1+json`


### Index file
- MUST exist
- MUST contain a OCI Image Index JSON object
- this image index contains references and descriptors for the image layout
- it is a multi-descriptor entry point
- provides an established path (`/index.json`) for an image-layout and auxiliary descriptors
- in general mediaType for each descriptor object in `manifests` object is one of the following
    - `application/vnd.oci.image.index.v1+json`
    - `application/vnd.oci.image.manifest.v1+json`
- future version may add new mediaTypes
- unknown mediaTypes SHOULD be ignored
- **Implementor's Note**: A common use case of descriptors with a "org.opencontainers.image.ref.name" annotation is representing a "tag" for a container image. For example, an image may have a tag for different versions or builds of the software. In the wild you often see "tags" like "v1.0.0-vendor.0", "2.0.0-debug", etc. Those tags will often be represented in an image-layout repository with matching "org.opencontainers.image.ref.name" annotations like "v1.0.0-vendor.0", "2.0.0-debug", etc.

## Filesystem Layer
- describes how to serialize a filesystem and filesystem changes like removed files into a blob called a layer
- one or more layers are applied on top of each other to create a complete filesystem
- defines the following `mediaTypes`:
    - `application/vnd.oci.image.layer.v1.tar`
        - layer changesets for this mediaType MUST be packaged in tar archive
        - layer changesets for this mediaType  MUST NOT include duplicate entries for file paths in resulting tar archive
    - `application/vnd.oci.image.layer.v1.tar+gzip`
        - this media type is gzip compressed `application/vnd.oci.image.layer.v1.tar` content
    - `application/vnd.oci.image.layer.nondistributable.v1.tar`
    - `application/vnd.oci.image.layer.nondistributable.v1.tar+gzip`
        - this media type is gzip compressed `application/vnd.oci.image.layer.nondistributable.v1.tar+gzip` content

### Change types
- types of changes that can occur in changesets:
    - additions
    - modifications
    - removals
- additions and modifications are represented the same in changeset archive
- removal is represented with "whiteout" files

### Supported files in changesets
- regular files
- directories
- sockets
- symbolic links
- block devices
- character devices
- FIFOs

### File attributes
- MUST be used where supported for addition and modifications
- modification time (mtime)
- user ID (uid)
    - user name (uname) secondary to uid
- group ID (gid )
    - group name (gname) secondary to gid
- mode (mode)
- extended attributes (xattrs)
- symlink reference (linkname + symbolic link type)
- hardlink reference (linkname)

## Image Configuration
 defines the `application/vnd.oci.image.config.v1+json` media type
- an ordered collection of root filesystem changes and the corresponding execution parameters for use within a container runtime
- outlines the JSON format describing images for use with a container runtime and execution tool and its relationship to filesystem changesets

### Layer
- set of filesystem changes relative to the parent layer
- doesn't have configuration data, those are properties of the whole image


### Image JSON
- describes basic information about the image
- references cryptographic hash of each layer used in the image
- considered immutable, changing this file implies changing imageID
- changing it means creating a new derived image, instead of changing the existing image


### Layer DiffID
- digest over the layer's uncompressed tar archive and serialized in the descriptor digest format ???
- NOTE: Do not confuse DiffIDs with layer digests, often referenced in the manifest, which are digests over compressed or uncompressed content

### Layer ChainID
- refer to a stack of layers with a single identifier
- definition
    ```
    ChainID(L₀) =  DiffID(L₀)
    ChainID(L₀|...|Lₙ₋₁|Lₙ) = Digest(ChainID(L₀|...|Lₙ₋₁) + " " + DiffID(Lₙ))
    ```
### ImageID
- given by the SHA256 hash of its configuration JSON
- represented as a hexadecimal encoding of 256 bits

## Conversion
- when extracting OCI image into OCI Runtime Bundle, two orthogonal components are relevant
    - extraction of the root filesystem from the set of filesystem layers
    - conversion from the image configuration blob to an OCI Runtime configuration blob
- converter MUST rely on the OCI image configuration to build the OCI runtime configuration; this will create the "default generated runtime configuration"
- "default generated runtime configuration" details
    - MAY be overridden or combined with externally provided inputs from the caller.
    - converter MAY have its own implementation-defined defaults and extensions which MAY be combined it

## Descriptor
- defines the `application/vnd.oci.descriptor.v1+json` media type.
- OCI image consists of several different components, arranged in a [Merkle Directed Acyclic Graph (DAG)](https://en.wikipedia.org/wiki/Merkle_tree)
- references between components in the graph are expressed through Content Descriptors
- Content Descriptor (or simply Descriptor) describes the disposition of the targeted content
- Content Descriptor includes the type of the content, a content identifier (digest), and the byte-size of the raw content
- Descriptors SHOULD be embedded in other formats to securely reference external content
- Other formats SHOULD use descriptors to securely reference external content

### Digests
- acts as a content identifier, enabling content-addressability
- digest string MUST match the following grammar:
    ```
    digest                ::= algorithm ":" encoded
    algorithm             ::= algorithm-component (algorithm-separator algorithm-component)*
    algorithm-component   ::= [a-z0-9]+
    algorithm-separator   ::= [+._-]
    encoded               ::= [a-zA-Z0-9=_-]+
    ```

## Links and resources
- [Specification](https://github.com/opencontainers/image-spec/blob/main/spec.md)
- [Image Media Types](https://github.com/opencontainers/image-spec/blob/v1.0.0/media-types.md)
- [Image Manifest](https://github.com/opencontainers/image-spec/blob/main/manifest.md)
- [Image Index](https://github.com/opencontainers/image-spec/blob/main/image-index.md)
- [Image Layout](https://github.com/opencontainers/image-spec/blob/main/image-layout.md)
- [Filesystem Layer](https://github.com/opencontainers/image-spec/blob/v1.0.0/layer.md)
- [Conversion](https://github.com/opencontainers/image-spec/blob/v1.0.0/conversion.md)
- [Descriptor](https://github.com/opencontainers/image-spec/blob/v1.0.0/descriptor.md)
- [Annotations](https://github.com/opencontainers/image-spec/blob/v1.0.0/annotations.md)

