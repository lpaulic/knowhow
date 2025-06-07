---
layout: default
title: West tool 
parent: Zephyr
nav_order: 1
---

# West - Zephyr meta-tool
{: .no_toc }

## Environment setup 

Setting up the build environment by using a docker image. The docker image for 
zephyr can be found on this Github repo: [Zephyr docker image](https://github.com/zephyrproject-rtos/docker-image).
After building the docker image following the instructions on the repo, 
setup the directory structure locally, i.e.:

```
    ~/zephyr-world         -> zephyr workspace for west
        |- zephyrproject    -> holds the zephyr workspace       
        |   |_ zephyr       -> holds the zephyr project
        |   ...    
        |_ app             -> directory holding application repos for freestadnig zephyr applications
            |_ ...
```

Commands for installing and running the docker container for zephyr:
```
# Replace the <tag> with a version to reference this build of zephyr build container
docker build -f Dockerfile.ci --build-arg UID=$(id -u) --build-arg GID=$(id -g) -t zephyr-build:v<tag> .

# Replace the <zephyr-development-workdir> with the location of the dir for zephyr stuff (i.e.: ~/zephyr-development)
docker run -ti --privileged -v <zephyr-development-workdir>:/workdir -v /dev:/dev zephyr-build:v<tag>
```

Commands for initializing zephyr in the docker:
```
west init /workdir/zephyrproject
cd /workdir/zephyrproject
west update
west zephyr-export
pip3 install --user -r /workdir/zephyrproject/zephyr/scripts/requirements.txt
```

Building a sample app:
```
cd /workdir/zephyrproject/zephyr
west -p auto -b esp32s3_devkitm sample/hello_world # works OK 
west -p auto -b esp32s3_devkitm sample/cpp/hello_world # have build issues with linker
```

Run on the board:
```
# In different terminal run serial terminal
picocom -b 115200 /dev/<serial-device>
weston flash
```

Building a standalone app:
- create an application folder anywhere
- position yourself in `<anywhere>`
- source the zephyr environment: `source /workdir/zephyrproject/zephyr/zephyr-env.sh`
    - use west
- floder structure can be found [here](https://docs.zephyrproject.org/latest/develop/application/index.html#zephyr-freestanding-application)
- passing CMake flags and options to west after specifying `--`  
- adding googletest to project, reference from [googletest github](https://github.com/google/googletest/blob/main/googletest/README.md):

```
include(FetchContent)
FetchContent_Declare(
  googletest
  # Specify the commit you depend on and update it regularly.
  URL https://github.com/google/googletest/archive/5376968f6948923e2411081fd9372e71a59d8e77.zip
)
# For Windows: Prevent overriding the parent project's compiler/linker settings
# set(gtest_force_shared_crt ON CACHE BOOL "" FORCE)
FetchContent_MakeAvailable(googletest)

add_executable(<project_exec_name> src/<source_file>)

target_link_libraries(<project_exec_name> PUBLIC
    gtest
    gtest_main
)

add_test(NAME <test_name> COMMAND <project_exec_name>)
```
- build the project using `native_posix` board 
- run tests with `cd build && ctest`

NOTE:
* issue with `std::cout` on xtensa architecture on 2024-02-23 [#66027](https://github.com/zephyrproject-rtos/zephyr/issues/66027)

## Links and resources:
- [West meta-tool](https://docs.zephyrproject.org/latest/develop/west/index.html)
- [Application samples and demos](https://docs.zephyrproject.org/latest/samples/index.html#samples-and-demos)
- [Application development](https://docs.zephyrproject.org/latest/develop/application/index.html#application)
- [Testing in zephyr](https://docs.zephyrproject.org/latest/develop/test/index.html)
- [Zephyr device tree mysteries solved](https://www.youtube.com/watch?v=w8GgP3h0M8M)
- [Zephyr YouTube channel - CircuitDojo](https://www.youtube.com/@CircuitDojo/streams)
- [Nordic Developer Academy](https://academy.nordicsemi.com)
