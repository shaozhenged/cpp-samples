# CPP API Sample

## Introduction

This repository contains a small example on how to use PLUX's CPP API to find, connect and adquire data, using either the internal bluetooth connection or using our [Fast USB Adapter](https://plux.info/biosignalsplux-accessories/371-fast-usb-data-transfer-cable-for-biosignalsplux-820201514.html) (only for Windows).

## Contents
In this repository you can find:
* The *.dlls* needed to comunicate with Fast USB Adaptor (windows only)
* plux.h - the header for plux's API
* simpleDev.cpp and .h - an example of a custom device implementation, which overload some of the base classes
* simpleApp.cpp - an example on how to find all PLUX's devices, connecting to one, configuring it, and start an acquisition
* CMakeLists.txt - Build configuration for CMake/Qt Creator

## Usage
To use this samples, simply clone this repository and link the correct *.lib/.a* for your operating system.
The API files can be found at this [link](https://downloads.plux.info/apis/PLUX-API-Cpp.zip), which support the following architectures:

* Win32/Win64 (VS2017)
* MacOS x86-64
* Linux x86-64

If you need the API compiled in other architectures, contact <support@plux.info>

## Building with Qt Creator

### Prerequisites
1. Install [Qt Creator](https://www.qt.io/download)
2. Download the PLUX API from [here](https://downloads.plux.info/apis/PLUX-API-Cpp.zip)
3. Extract the API files and place the appropriate library file in the `/lib` folder:
   - For Windows 32-bit: `plux.lib`
   - For Windows 64-bit: `plux64.lib`
   - For macOS: `libplux.a`
   - For Linux: `libplux.a`

### Steps to Build
1. Open Qt Creator
2. Select "Open Project" and navigate to the CMakeLists.txt file in this repository
3. Configure the project for your desired build configuration (Debug/Release)
4. Click "Build" to compile the project
5. Run the application

### Notes for Windows Users
- The required DLL files for the Fast USB Adapter (LibFT4222.dll, LibFT4222-64.dll, etc.) will be automatically copied to the build directory
- Make sure you have the Visual C++ Redistributable packages installed on your system
