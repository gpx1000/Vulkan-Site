# Portability Initiative

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/portability_initiative.html

## Table of Contents

- [Translation Layer](#_translation_layer)
- [MacOS and iOS Tools](#_macos_and_ios_tools)
- [MacOS_and_iOS_Tools](#_macos_and_ios_tools)
- [gfx-rs](#_gfx_rs)

## Content

Notice Currently a provisional VK_KHR_portability_subset extension specification is available with the vulkan_beta.h headers. More information can found in the press release. The Vulkan Portability Initiative is an effort inside the Khronos Group to develop resources to define and evolve the subset of Vulkan capabilities that can be made universally available at native performance levels across all major platforms, including those not currently served by Vulkan native drivers. In a nutshell, this initiative is about making Vulkan viable on platforms that do not natively support the API (e.g MacOS and iOS). Layered implementations fight industry fragmentation by enabling more applications to run on more platforms, even in a fragmented industry API landscape. For example, the first row in the diagram below shows how Vulkan is being used as a porting target to bring additional APIs to platforms to enable more content without the need for additional kernel-level drivers. Layered API implementations have been used to successfully ship production applications on multiple platforms. The columns in the figure show layering projects being used to make APIs available across additional platforms, even if no native drivers are available, giving application developers the deployment flexibility they need to develop with the graphics API of their choice and ship across multiple platforms. The first column in the diagram is the work of the Vulkan Portability Initiative, enabling layered implementations of Vulkan functionality across diverse platforms. Khronos Blog for information about macOS and iOS support Mozilla is currently helping drive gfx-rs portability to use gfx-hal as a way to interface with various other APIs.
