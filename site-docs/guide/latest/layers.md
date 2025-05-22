# Layers

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/layers.html

## Table of Contents

- [Using Layers](#_using_layers)
- [Vulkan Configurator Tool](#_vulkan_configurator_tool)
- [Vulkan_Configurator_Tool](#_vulkan_configurator_tool)
- [Device Layers Deprecation](#_device_layers_deprecation)
- [Device_Layers_Deprecation](#_device_layers_deprecation)
- [Creating a Layer](#_creating_a_layer)
- [Creating_a_Layer](#_creating_a_layer)
- [Platform Variations](#_platform_variations)
- [Android](#_android)
- [Linux](#_linux)
- [MacOS](#_macos)
- [Windows](#_windows)

## Content

Layers are optional components that augment the Vulkan system. They can intercept, evaluate, and modify existing Vulkan functions on their way from the application down to the hardware. Layer properties can be queried from an application with [vkEnumerateInstanceLayerProperties](https://docs.vulkan.org/spec/latest/chapters/extensions.html#vkEnumerateInstanceLayerProperties).

Layers are packaged as shared libraries that get dynamically loaded in by the loader and inserted between it and the application. The two things needed to use layers are the location of the binary files and which layers to enable. The layers to use can be either explicitly enabled by the application or implicitly enabled by telling the loader to use them. More details about implicit and explicit layers can be found in the [Loader and Layer Interface](https://github.com/KhronosGroup/Vulkan-Loader/blob/main/docs/LoaderApplicationInterface.md#implicit-vs-explicit-layers).

The [Vulkan SDK](https://vulkan.lunarg.com/sdk/home) contains a [layer configuration document](https://vulkan.lunarg.com/doc/sdk/latest/windows/layer_configuration.html) that is very specific to how to discover and configure layers on each of the platforms.

Developers on Windows, Linux, and macOS can use the Vulkan Configurator, vkconfig, to enable explicit layers and disable implicit layers as well as change layer settings from a graphical user interface.
Please see the [Vulkan Configurator documentation](https://vulkan.lunarg.com/doc/sdk/latest/windows/vkconfig.html) in the Vulkan SDK for more information on using the Vulkan Configurator.

There used to be both instance layers and device layers, but device layers were [deprecated](https://docs.vulkan.org/spec/latest/chapters/extensions.html#extendingvulkan-layers-devicelayerdeprecation) early in Vulkan’s life and should be avoided.

Anyone can create a layer as long as it follows the [loader to layer interface](https://github.com/KhronosGroup/Vulkan-Loader/blob/main/docs/LoaderApplicationInterface.md#loader-and-layer-interface) which is how the loader and layers agree to communicate with each other.

The way to load a layer in implicitly varies between loader and platform.

As of Android P (Android 9 / API level 28), if a device is in a debuggable state such that `getprop ro.debuggable` [/data/local/debug/vulkan](https://cs.android.com/android/platform/superproject//android-9.0.0_r1:frameworks/native/vulkan/libvulkan/layers_extensions.cpp;l=454[returns 1], then the loader will look in link:https://cs.android.com/android/platform/superproject//android-9.0.0_r1:frameworks/native/vulkan/libvulkan/layers_extensions.cpp;l=67).

Starting in Android P (Android 9 / API level 28) implicit layers can be [pushed using ADB](https://developer.android.com/ndk/guides/graphics/validation-layer#vl-adb) if the application was built in debug mode.

There is no way other than the options above to use implicit layers.

The [Vulkan SDK](https://vulkan.lunarg.com/doc/sdk/latest/linux/layer_configuration.html) explains how to use implicit layers on Linux.

The [Vulkan SDK](https://vulkan.lunarg.com/doc/sdk/latest/mac/layer_configuration.html) explains how to use implicit layers on MacOS.

The [Vulkan SDK](https://vulkan.lunarg.com/doc/sdk/latest/windows/layer_configuration.html) explains how to use implicit layers on Windows.
