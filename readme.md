# Installation

## conan
This program relies on the Conan package manager to install the Boost, Eigen, and Nlohmann JSON libraries. Installing Conan is
not required if you have these libraries already and CMake can find them.
1. [Install Conan](https://docs.conan.io/2/installation.html)
2. Generate a Conan profile by running `conan profile detect --force`
3. The generated profile (located in `~/.conan2/profiles`) should resemble
   ```
   [settings]
   arch=x86_64
   build_type=Release
   compiler=gcc
   compiler.cppstd=gnu14
   compiler.libcxx=libstdc++11
   compiler.version=11
   os=Linux
   ```
4. `cd` into working directory
5. `conan install . -pr:b=default --output-folder=build --build=missing`

## I2SL Repos
Clone the `Event Sensor Detection and Tracking` and `stage-camera` repositories into the working directory:
1. `cd .../Live-EBS-Tracking`
2. `gh repo clone I2SL/Event-Sensor-Detection-and-Tracking`
3. `gh repo clone I2SL/stage-camera`

## FLIR PTU-SDK
The FLIR PTU-SDK is proprietary and must be purchased prior to running this program. Once the SDK libraries are built
according to the provided instructions, create a folder named `ptu-sdk` in the working directory. Then put the contents
of the PTU-SDK in this folder so that `cpi.h`, `libcpi.a`, `cerial/`, and `examples/` are directly under the `ptu-sdk/`
directory. This program uses PTU-SDK version `2.0.4`.

## mlpack
`mlpack` should be built and installed by following the instructions on the [GitHub page](https://github.com/mlpack/mlpack).

## OpenCV
OpenCV should be installed by following the instructions on [their website](https://docs.opencv.org/4.x/d7/d9f/tutorial_linux_install.html).
It should be installed **with contributions**.

## libcaer
The `libcaer` library should be installed by following the instructions found on their [GitLab page](https://gitlab.com/inivation/dv/libcaer).

## VimbaCPP
The Vimba SDK is used to communicate with an Allied Vision 1800 U-500. First, install the SDK by following the instructions on [their website](https://www.alliedvision.com/en/products/vimba-sdk/). If needed, modify the directories in `FindVimbaCPP.cmake` (located under `cmake/modules`) to link to the library.

## Build
When the all the dependencies above are installed, you can build by running:
1. `cd build`
2. `cmake -DCMAKE_C_COMPILER=gcc-11 -DCMAKE_CXX_COMPILER=g++-11 -DCMAKE_TOOLCHAIN_FILE=conan_toolchain.cmake -DCMAKE_BUILD_TYPE=Release ..`
3. `make`

## Usage
To run the program, enter the following command in the terminal: `./LiveTracking -p tcp:<FLIR IP ADDR> <PATH TO CONFIG JSON> <PATH TO ONNX FILE>`.
The program expects three arguments even when the stage is not in use. If the FLIR stage is not present, or you do not
want to enable it, you should adjust the appropriate setting in the JSON file but still enter three arguments in the
terminal. In this case, the content of the first two arguments will not matter.

## References
1. https://gist.github.com/Yousha/3830712334ac30a90eb6041b932b68d7
2. https://gitlab.com/inivation/dv/libcaer
3. https://docs.opencv.org/4.x/d7/d9f/tutorial_linux_install.html
4. https://github.com/mlpack/mlpack
5. https://docs.conan.io/2/installation.html
6. https://github.com/gipert/progressbar