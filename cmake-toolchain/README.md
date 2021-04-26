# Cross Compiliation
 **Notice:** Running the AWS IoT Device Client will incur usage of AWS IoT services, and is likely to incur charges on your AWS account. Please refer the pricing pages for [AWS IoT Core](https://aws.amazon.com/iot-core/pricing/), [AWS IoT Device Management](https://aws.amazon.com/iot-device-management/pricing/), and [AWS IoT Device Defender](https://aws.amazon.com/iot-device-defender/pricing/) for more details.

[*Back To The Main Readme*](../README.md)

## Building from one architecture to the other

**Description**:
Cross-compiling allows you to compile for a **specific architecture** while on a **different architecture**, for exmaple you may want to compile the Device Client for a Raspberry Pi (ARMhf) using cmake toolchains you could compile the binary on your laptop (x86_64) and then tranfer it over.  This is extremely useful, as some *(Especially really constrained)* devices won't have the resources to complete the build process.  Even if your devices can complete the build, it is often times much easier to build in a central location (like your developer laptop) and then distribute the artifacts to appropriate devices. 

The `cmake-toolchain` folder contains toolchains files that will make cross compiling for other architectures easier (This does not include the compilers). Currently we have toolchain files to support cross compiling for the following architectures; **MIPS32**, **ARMhf**, andx **AArch64**.

You can specify one of the given build toolchains when running cmake:
```
cmake ../ -DCMAKE_TOOLCHAIN_FILE=<Path/To/Build/Toolchain/File>
```
This will allow the toolchain files to overwrite variables *(various paths, compilers, and flags)* required to execute cross compilation without changing the original **cmake** file.

**Dependencies**:
For your build to be successful you'll also need a cross compiled version of our dependency ([aws-iot-device-sdk-cpp-v2](https://github.com/aws/aws-iot-device-sdk-cpp-v2)), for the SDK this is automatically accomplished when running the **cmake** command above without the following flag `-DBUILD_SDK=OFF`.
```
cmake ../ -DCMAKE_TOOLCHAIN_FILE=<Path/To/Build/Toolchain/File>
```

For a real example look into our [.github/build.sh](../.github/build.sh) script.

**Other Architecture**:
If you need to compile for an architecture that isn't currently supported, then you can create a new toolchain files based on the sample toolchains included in the cmake-toolchain folder.

[*Back To The Top*](#cross-compilation)