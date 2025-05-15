# Loader

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/loader.html

## Table of Contents

- [Linking Against the Loader](#_linking_against_the_loader)
- [Linking_Against_the_Loader](#_linking_against_the_loader)
- [Platform Variations](#_platform_variations)
- [Android](#_android)
- [Linux](#_linux)
- [MacOS](#_macos)
- [Windows](#_windows)

## Content

The loader is responsible for mapping an application to Vulkan layers and Vulkan installable client drivers (ICD). Anyone can create their own Vulkan Loader, as long as they follow the Loader Interface. One can build the reference loader as well or grab a built version from the Vulkan SDK for selected platforms. The Vulkan headers only provide the Vulkan function prototypes. When building a Vulkan application you have to link it to the loader or you will get errors about undefined references to the Vulkan functions. There are two ways of linking the loader, directly and indirectly, which should not be confused with “static and dynamic linking”. Directly linking at compile time This requires having a built Vulkan Loader (either as a static or dynamic library) that your build system can find. Build systems (Visual Studio, CMake, etc) have documentation on how to link to the library. Try searching “(InsertBuildSystem) link to external library” online. Indirectly linking at runtime Using dynamic symbol lookup (via system calls such as dlsym and dlopen) an application can initialize its own dispatch table. This allows an application to fail gracefully if the loader cannot be found. It also provides the fastest mechanism for the application to call Vulkan functions. Volk is an open source implementation of a meta-loader to help simplify this process. Each platform can set its own rules on how to enforce the Vulkan Loader. Android devices supporting Vulkan provide a Vulkan loader already built into the OS. A vulkan_wrapper.c/h file is provided in the Android NDK for indirectly linking. This is needed, in part, because the Vulkan Loader can be different across different vendors and OEM devices. The Vulkan SDK provides a pre-built loader for Linux. The Getting Started page in the Vulkan SDK explains how the loader is found on Linux. The Vulkan SDK provides a pre-built loader for MacOS The Getting Started page in the Vulkan SDK explains how the loader is found on MacOS. The Vulkan SDK provides a pre-built loader for Windows. The Getting Started page in the Vulkan SDK explains how the loader is found on Windows.
