---
layout: default
title: Bash Script Templates
parent: Templates
nav_order: 5
---

# Bash shell script
{: .no_toc }

```
#!/bin/env bash

### Metadata ###
# Description: Script for updating the cellular modem. Accepts the 
#              absolute path to the directory holding the firmware
#              update files.

### Error Flags ###
set -eo pipefail

### Trap Handling ###
interrupt_trap() {
    echo "INFO: cleanup interrupt call"
    error_cleanup
}

trap interrupt_trap SIGINT

### Function Definition ###
usage() {
    echo "Usage: $0 [options] <argument>"
    echo
    echo "Flags:"
    echo "  options             Optional flags. Must be one of:"
    echo "                      -h|--help"
    echo
    echo "Arguments:"
    echo "  argument            Mandatory argument."
}

cleanup() {
}

error_cleanup() {
}

### Default Values ###
SHORT_OPTS="h"
LONG_OPTS="help,example:"

### Source scripts ###

### Command Line Flags Parsing ###
if ! TEMP=$(getopt -o "${SHORT_OPTS}" -l "${LONG_OPTS}" -n "$0" -- "$@"); then
    echo "ERR: Failed to parse arguments."
    usage
    exit 1
fi

eval set -- "$TEMP"
while true; do
    case "$1" in
        -h|--help)
            usage
            exit 0
            ;;
        --example)
            # NOTE: do something
            shift 2
            ;;
        --)
            shift
            break
            ;;
        *)
            echo "ERR: Unexpected option $1"
            usage
            exit 1
            ;;
    esac
done

# NOTE: additional checks for flag options go here

### Command Line Arguments parsing ###

### Main Script Logic ###

# NOTE: cleanup is not necessary
cleanup

exit 0
```

