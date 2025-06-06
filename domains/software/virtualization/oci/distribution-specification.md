---
layout: default
title: Distribution Specification 
parent: Open Container Initiative 
nav_order: 1
---

# OCI Distribution Specification
{: .no_toc }

## Overview
- defines an API protocol to facilitate and standardize the distribution of content
- based on the specification for the [Docker Registry HTTP API V2 protocol](https://github.com/distribution/distribution/blob/5cb406d511b7b9163bff9b6439072e4892e5ae3b/docs/spec/api.md)
- definitions
    - ***Registry***: a service that handles the required APIs defined in this specification
    - ***Client***: a tool that communicates with Registries
    - ***Push***: the act of uploading Blobs and Manifests to a Registry
    - ***Pull***: the act of downloading Blobs and Manifests from a Registry
    - ***Blob***: the binary form of content that is stored by a Registry, addressable by a Digest
    - ***Manifest***: a JSON document which defines an artifact uploaded via the manifests endpoint. A manifest may reference other blobs in a repository via descriptors.
    - ***Config***: a blob referenced in the Manifest which contains Artifact metadata.
    - ***Artifact***: one conceptual piece of content stored as Blobs with an accompanying Manifest containing a Config
    - ***Digest***: a unique identifier created from a cryptographic hash of a Blob's content.
    - ***Tag***: a custom, human-readable Manifest identifier

## Conformance

### Workflow categories

#### Pull
- pulling manifests
    - process of pulling an artifact centers around retrieving two components: the manifest and one or more blobs
    - the first step in pulling an artifact is to retrieve the manifest.
        - however, you MAY retrieve content from the registry in any order.
    - to pull a manifest perform a `GET` request to a URL in the format: `/v2/<name>/manifests/<reference>`
        - `<name>`
            - refers to namespace of the repository
            - namespace/repository
            - MUST match the regular expression: `[a-z0-9]+([._-][a-z0-9]+)*(/[a-z0-9]+([._-][a-z0-9]+)*)*`
        - `<reference>`
            - must be on of the following
                - (a) digest of a manifest
                - (b) a tag
            - MUST not be in any other format
                - MUST be at most 128 characters in length
                - MUST match the following regular expression: `[a-zA-Z0-9_][a-zA-Z0-9._-]{0,127}`

- pulling blobs
    - to pull a blob perform a `GET` request to a URL in the following form: `/v2/<name>/blobs/<digest>`
        - `<name>`
            - the namespace of the repository
            - commonly has a from of  namespace/repository
        - `<digest>`
            - blob's digest

- checking if content exists in the registry
    - to verify that a repository contains a given manifest or blob, make a `HEAD` request to a URL in the following form
        - for manifest `/v2/<name>/manifests/<reference>`
        - for blob `/v2/<name>/blobs/<digest>`

## Links and resources
- [Specification](https://github.com/opencontainers/distribution-spec/blob/main/spec.md)

