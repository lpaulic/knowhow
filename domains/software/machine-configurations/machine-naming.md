---
layout: default
title: Machine Naming Convention
parent: Machine Configurations
nav_order: 1
---

# Machine naming convention
{: .no_toc }

For personal work machines I am naming the macines 
using tree names, i.e.: oak, olive, pine, etc. No specific 
reason other that it sounds good and there are plenty of 
trees so I will not run out of names.

The machine name represents the following machine configurations:
- CPU
- GPU
- OS
- Desktop environment

The machine name follows the following template:
```
<profile-name>-<4-digit-SN>
```

Differences in above components differentiate the machine configurations,
if two machines have the same above components they will have the 
same profile name name. Each machine will have its own SN. 

Current machine profiles that I am using or have configured:
- `bonsai`:
    - Windows WSL distribution
    - OS: Arch Linux
    - Desktop environemnt: Headless
- `ginkgo`:
    - CPU: AMD
    - GPU: AMD
    - OS: Arch Linux
    - Desktop environment: Hyprland
- `maple`:
    - CPU: AMD
    - GPU: AMD + NVIDIA
    - OS: Arch Linux
    - Desktop environment: Hyprland

The utilization of the naming scheem can be found on my personal 
dotfiles repository: [dotfiles](https://github.com/lpaulic/dotfiles)
