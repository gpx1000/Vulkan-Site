# Versions

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/versions.html

## Table of Contents

- [Instance and Device](#_instance_and_device)
- [Instance_and_Device](#_instance_and_device)
- [Header](#_header)
- [Extensions](#_extensions)
- [Structs and enums](#_structs_and_enums)
- [Structs_and_enums](#_structs_and_enums)
- [Functions](#_functions)
- [Features](#_features)
- [Limits](#_limits)
- [SPIR-V](#_spir_v)

## Content

Vulkan works on a [major, minor, patch](https://docs.vulkan.org/spec/latest/chapters/extensions.html#extendingvulkan-coreversions-versionnumbers) versioning system. Currently, there are 3 minor version releases of Vulkan (1.0, 1.1, 1.2 and 1.3) which are backward compatible with each other. An application can use [vkEnumerateInstanceVersion](https://docs.vulkan.org/spec/latest/chapters/initialization.html#vkEnumerateInstanceVersion) to check what version of a Vulkan instance is supported. There is also a [white paper](https://www.lunarg.com/wp-content/uploads/2019/02/Vulkan-1.1-Compatibility-Statement_01_19.pdf) by LunarG on how to query and check for the supported version. While working across minor versions, there are some subtle things to be aware of.

It is important to remember there is a difference between the instance-level version and device-level version. It is possible that the loader and implementations will support different versions.

The [Querying Version Support](https://docs.vulkan.org/spec/latest/chapters/extensions.html#extendingvulkan-coreversions-queryingversionsupport) section in the Vulkan Spec goes into details on how to query for supported versions at both the instance and device level.

There is only one supported header for all major releases of Vulkan. This means that there is no such thing as “Vulkan 1.0 headers” as all headers for a minor and patch version are unified. This should not be confused with the ability to generate a 1.0 version of the [Vulkan Spec](vulkan_spec.html#vulkan-spec), as the Vulkan Spec and header of the same patch version will match. An example would be that the generated 1.0.42 Vulkan Spec will match the 1.x.42 header.

It is highly recommended that developers try to keep up to date with the latest header files released. The Vulkan SDK comes in many versions which map to the header version it will have been packaged for.

Between minor versions of Vulkan, [some extensions](https://docs.vulkan.org/spec/latest/appendices/versions.html#versions-1.1) get [promoted](https://docs.vulkan.org/spec/latest/chapters/extensions.html#extendingvulkan-compatibility-promotion) to the [core version](https://docs.vulkan.org/spec/latest/chapters/extensions.html#extendingvulkan-coreversions). When targeting a newer minor version of Vulkan, an application will not need to enable the newly promoted extensions at the instance and device creation. However, if an application wants to keep backward compatibility, it will need to enable the extensions.

For a summary of what is new in each version, check out the [Vulkan Release Summary](vulkan_release_summary.html#vulkan-release-summary)

Structs and enums are dependent on the header file being used and not the version of the instance or device queried. For example, the struct `VkPhysicalDeviceFeatures2` used to be `VkPhysicalDeviceFeatures2KHR` before Vulkan 1.1 was released. Regardless of the 1.x version of Vulkan being used, an application should use `VkPhysicalDeviceFeatures2` in its code as it matches the newest header version. For applications that did have `VkPhysicalDeviceFeatures2KHR` in the code, there is no need to worry as the Vulkan header also aliases any promoted structs and enums (`typedef VkPhysicalDeviceFeatures2 VkPhysicalDeviceFeatures2KHR;`).

The reason for using the newer naming is that the Vulkan Spec itself will only refer to `VkPhysicalDeviceFeatures2` regardless of what version of the Vulkan Spec is generated. Using the newer naming makes it easier to quickly search for where the structure is used.

Since functions are used to interact with the loader and implementations, there needs to be a little more care when working between minor versions. As an example, let’s look at `vkGetPhysicalDeviceFeatures2KHR` which was promoted to core as `vkGetPhysicalDeviceFeatures2` from Vulkan 1.0 to Vulkan 1.1. Looking at the Vulkan header both are declared.

typedef void (VKAPI_PTR *PFN_vkGetPhysicalDeviceFeatures2)(VkPhysicalDevice physicalDevice, VkPhysicalDeviceFeatures2* pFeatures);
// ...
typedef void (VKAPI_PTR *PFN_vkGetPhysicalDeviceFeatures2KHR)(VkPhysicalDevice physicalDevice, VkPhysicalDeviceFeatures2* pFeatures);

The main difference is when calling `vkGetInstanceProcAddr(instance, “vkGetPhysicalDeviceFeatures2”);` a Vulkan 1.0 implementation may not be aware of `vkGetPhysicalDeviceFeatures2` existence and `vkGetInstanceProcAddr` will return `NULL`. To be backward compatible with Vulkan 1.0 in this situation, the application should query for `vkGetPhysicalDeviceFeatures2KHR` as a 1.1 Vulkan implementation will likely have the function directly pointed to the `vkGetPhysicalDeviceFeatures2` function pointer internally.

Between minor versions, it is possible that some feature bits are added, removed, made optional, or made mandatory. All details of features that have changed are described in the [Core Revisions](https://docs.vulkan.org/spec/latest/appendices/versions.html) section.

The [Feature Requirements](https://docs.vulkan.org/spec/latest/chapters/features.html#features-requirements) section in the Vulkan Spec can be used to view the list of features that are required from implementations across minor versions.

Currently, all versions of Vulkan share the same minimum/maximum limit requirements, but any changes would be listed in the [Limit Requirements](https://docs.vulkan.org/spec/latest/chapters/limits.html#limits-minmax) section of the Vulkan Spec.

Every minor version of Vulkan maps to a version of [SPIR-V that must be supported](https://docs.vulkan.org/spec/latest/appendices/spirvenv.html).

* 
Vulkan 1.0 supports SPIR-V 1.0

* 
Vulkan 1.1 supports SPIR-V 1.3 and below

* 
Vulkan 1.2 supports SPIR-V 1.5 and below

* 
Vulkan 1.3 supports SPIR-V 1.6 and below

It is up to the application to make sure that the SPIR-V in `VkShaderModule` is of a valid version to the corresponding Vulkan version.
