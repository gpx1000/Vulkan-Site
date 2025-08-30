# VkRenderingFlagBits(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkRenderingFlagBits.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkRenderingFlagBits - Bitmask specifying additional properties of a dynamic render pass instance

Bits which **can** be set in [VkRenderingInfo](VkRenderingInfo.html)::`flags` describing
additional properties of the render pass are:

// Provided by VK_VERSION_1_3
typedef enum VkRenderingFlagBits {
    VK_RENDERING_CONTENTS_SECONDARY_COMMAND_BUFFERS_BIT = 0x00000001,
    VK_RENDERING_SUSPENDING_BIT = 0x00000002,
    VK_RENDERING_RESUMING_BIT = 0x00000004,
  // Provided by VK_EXT_legacy_dithering with (VK_KHR_dynamic_rendering or VK_VERSION_1_3) and (VK_KHR_maintenance5 or VK_VERSION_1_4)
    VK_RENDERING_ENABLE_LEGACY_DITHERING_BIT_EXT = 0x00000008,
  // Provided by VK_KHR_maintenance7
    VK_RENDERING_CONTENTS_INLINE_BIT_KHR = 0x00000010,
  // Provided by VK_VALVE_fragment_density_map_layered
    VK_RENDERING_PER_LAYER_FRAGMENT_DENSITY_BIT_VALVE = 0x00000020,
  // Provided by VK_KHR_dynamic_rendering
    VK_RENDERING_CONTENTS_SECONDARY_COMMAND_BUFFERS_BIT_KHR = VK_RENDERING_CONTENTS_SECONDARY_COMMAND_BUFFERS_BIT,
  // Provided by VK_KHR_dynamic_rendering
    VK_RENDERING_SUSPENDING_BIT_KHR = VK_RENDERING_SUSPENDING_BIT,
  // Provided by VK_KHR_dynamic_rendering
    VK_RENDERING_RESUMING_BIT_KHR = VK_RENDERING_RESUMING_BIT,
  // Provided by VK_EXT_nested_command_buffer
    VK_RENDERING_CONTENTS_INLINE_BIT_EXT = VK_RENDERING_CONTENTS_INLINE_BIT_KHR,
} VkRenderingFlagBits;

or the equivalent

// Provided by VK_KHR_dynamic_rendering
typedef VkRenderingFlagBits VkRenderingFlagBitsKHR;

* 
`VK_RENDERING_CONTENTS_SECONDARY_COMMAND_BUFFERS_BIT` specifies that
draw calls for the render pass instance will be recorded in secondary
command buffers.
If the [`nestedCommandBuffer`](../../../../spec/latest/chapters/features.html#features-nestedCommandBuffer)
feature is enabled, the draw calls **can** come from both inline and
[vkCmdExecuteCommands](vkCmdExecuteCommands.html).

* 
`VK_RENDERING_RESUMING_BIT` specifies that the render pass instance
is resuming an earlier suspended render pass instance.

* 
`VK_RENDERING_SUSPENDING_BIT` specifies that the render pass
instance will be suspended.

* 
`VK_RENDERING_ENABLE_LEGACY_DITHERING_BIT_EXT` specifies that
[Legacy Dithering](../../../../spec/latest/chapters/interfaces.html#interfaces-legacy-dithering) is enabled for the
render pass instance.

* 
`VK_RENDERING_CONTENTS_INLINE_BIT_KHR` specifies that draw calls for
the render pass instance **can** be recorded inline within the current
command buffer.
This **can** be combined with the
`VK_RENDERING_CONTENTS_SECONDARY_COMMAND_BUFFERS_BIT` bit to allow
draw calls to be recorded both inline and in secondary command buffers.

* 
`VK_RENDERING_PER_LAYER_FRAGMENT_DENSITY_BIT_VALVE` specifies that
the render pass **can** be used with layered fragment density maps.

The contents of `pRenderingInfo` **must** match between suspended render
pass instances and the render pass instances that resume them, other than
the presence or absence of the `VK_RENDERING_RESUMING_BIT`,
`VK_RENDERING_SUSPENDING_BIT`, and
`VK_RENDERING_CONTENTS_SECONDARY_COMMAND_BUFFERS_BIT` flags.
No action or synchronization commands, or other render pass instances, are
allowed between suspending and resuming render pass instances.

[VK_KHR_dynamic_rendering](VK_KHR_dynamic_rendering.html), [VK_VERSION_1_3](VK_VERSION_1_3.html), [VkRenderingFlags](VkRenderingFlags.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/renderpass.html#VkRenderingFlagBits).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
