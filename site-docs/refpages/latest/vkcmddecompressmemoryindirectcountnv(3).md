# vkCmdDecompressMemoryIndirectCountNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/vkCmdDecompressMemoryIndirectCountNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Parameters](#_parameters)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

vkCmdDecompressMemoryIndirectCountNV - Indirect decompress data between memory regions

To decompress data between one or more memory regions by specifying
decompression parameters indirectly in a buffer, call:

// Provided by VK_NV_memory_decompression
void vkCmdDecompressMemoryIndirectCountNV(
    VkCommandBuffer                             commandBuffer,
    VkDeviceAddress                             indirectCommandsAddress,
    VkDeviceAddress                             indirectCommandsCountAddress,
    uint32_t                                    stride);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`indirectCommandsAddress` is the device address containing
decompression parameters laid out as an array of
[VkDecompressMemoryRegionNV](VkDecompressMemoryRegionNV.html) structures.

* 
`indirectCommandsCountAddress` is the device address containing the
decompression count.

* 
`stride` is the byte stride between successive sets of decompression
parameters located starting from `indirectCommandsAddress`.

Each region specified in `indirectCommandsAddress` is decompressed from
the source to destination region based on the specified decompression
method.

Valid Usage

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-None-07692) VUID-vkCmdDecompressMemoryIndirectCountNV-None-07692

The [`memoryDecompression`](../../../../spec/latest/chapters/features.html#features-memoryDecompression) feature
**must** be enabled

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-07694) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-07694

The [VkBuffer](VkBuffer.html) that `indirectCommandsAddress` comes from **must**
have been created with the `VK_BUFFER_USAGE_INDIRECT_BUFFER_BIT` bit
set

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-offset-07695) VUID-vkCmdDecompressMemoryIndirectCountNV-offset-07695

`offset` **must** be a multiple of `4`

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07697) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07697

The [VkBuffer](VkBuffer.html) that `indirectCommandsCountAddress` comes from
**must** have been created with the
`VK_BUFFER_USAGE_INDIRECT_BUFFER_BIT` bit set

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07698) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07698

`indirectCommandsCountAddress` **must** be a multiple of `4`

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07699) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07699

The count stored in `indirectCommandsCountAddress` **must** be less
than or equal to
`VkPhysicalDeviceMemoryDecompressionPropertiesNV`::`maxDecompressionIndirectCount`

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-stride-07700) VUID-vkCmdDecompressMemoryIndirectCountNV-stride-07700

`stride` **must** be a multiple of `4` and **must** be greater than or
equal to sizeof(`VkDecompressMemoryRegionNV`)

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07701) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07701

If the count stored in `indirectCommandsCountAddress` is equal to
`1`, (`offset` + 
sizeof(`VkDecompressMemoryRegionNV`)) **must** be less than or equal
to the size of the [VkBuffer](VkBuffer.html) that `indirectCommandsAddress`
comes from

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07702) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07702

If the count stored in `indirectCommandsCountAddress` is greater
than `1`, `indirectCommandsAddress` + 
sizeof(`VkDecompressMemoryRegionNV`) +  (`stride`
× (count stored in `countBuffer` - 1)) **must** be less than or
equal to the last valid address in the [VkBuffer](VkBuffer.html) that
`indirectCommandsAddress` was created from

Valid Usage (Implicit)

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-parameter) VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](VkCommandBuffer.html) handle

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-parameter) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-parameter

 `indirectCommandsAddress` **must** be a valid `VkDeviceAddress` value

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-parameter) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-parameter

 `indirectCommandsCountAddress` **must** be a valid `VkDeviceAddress` value

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-recording) VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](../../../../spec/latest/chapters/cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-cmdpool) VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics, or compute operations

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-renderpass) VUID-vkCmdDecompressMemoryIndirectCountNV-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-videocoding) VUID-vkCmdDecompressMemoryIndirectCountNV-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties
| [Command Buffer Levels](../../../../spec/latest/chapters/cmdbuffers.html#VkCommandBufferLevel) | [Render Pass Scope](../../../../spec/latest/chapters/renderpass.html#vkCmdBeginRenderPass) | [Video Coding Scope](../../../../spec/latest/chapters/videocoding.html#vkCmdBeginVideoCodingKHR) | [Supported Queue Types](../../../../spec/latest/chapters/devsandqueues.html#VkQueueFlagBits) | [Command Type](../../../../spec/latest/chapters/fundamentals.html#fundamentals-queueoperation-command-types) |
| --- | --- | --- | --- | --- |
| Primary

Secondary | Outside | Outside | Graphics

Compute | Action |

Conditional Rendering

vkCmdDecompressMemoryIndirectCountNV is not affected by [conditional rendering](../../../../spec/latest/chapters/drawing.html#drawing-conditional-rendering)

[VK_NV_memory_decompression](VK_NV_memory_decompression.html), [VkCommandBuffer](VkCommandBuffer.html), `VkDeviceAddress`

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/VK_NV_memory_decompression.html#vkCmdDecompressMemoryIndirectCountNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
