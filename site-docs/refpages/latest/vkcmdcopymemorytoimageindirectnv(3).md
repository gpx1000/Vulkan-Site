# vkCmdCopyMemoryToImageIndirectNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/vkCmdCopyMemoryToImageIndirectNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Parameters](#_parameters)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

vkCmdCopyMemoryToImageIndirectNV - Copy data from a memory region into an image

To copy data from a memory region to an image object by specifying copy
parameters in a buffer, call:

// Provided by VK_NV_copy_memory_indirect
void vkCmdCopyMemoryToImageIndirectNV(
    VkCommandBuffer                             commandBuffer,
    VkDeviceAddress                             copyBufferAddress,
    uint32_t                                    copyCount,
    uint32_t                                    stride,
    VkImage                                     dstImage,
    VkImageLayout                               dstImageLayout,
    const VkImageSubresourceLayers*             pImageSubresources);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`copyBufferAddress` is the buffer address specifying the copy
parameters.
This buffer is laid out in memory as an array of
[VkCopyMemoryToImageIndirectCommandNV](VkCopyMemoryToImageIndirectCommandNV.html) structures.

* 
`copyCount` is the number of copies to execute, and can be zero.

* 
`stride` is the byte stride between successive sets of copy
parameters.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the copy.

* 
`pImageSubresources` is a pointer to an array of size
`copyCount` of [VkImageSubresourceLayers](VkImageSubresourceLayers.html) used to specify the
specific image subresource of the destination image data for that copy.

Each region in `copyBufferAddress` is copied from the source memory
region to an image region in the destination image.
If the destination image is of type `VK_IMAGE_TYPE_3D`, the starting
slice and number of slices to copy are specified in
`pImageSubresources->baseArrayLayer` and
`pImageSubresources->layerCount` respectively.
The copy **must** be performed on a queue that supports indirect copy
operations, see [VkPhysicalDeviceCopyMemoryIndirectPropertiesNV](VkPhysicalDeviceCopyMemoryIndirectPropertiesNV.html).

Valid Usage

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-None-07660) VUID-vkCmdCopyMemoryToImageIndirectNV-None-07660

The [`indirectCopy`](../../../../spec/latest/chapters/features.html#features-indirectCopy) feature **must** be
enabled

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07661) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07661

`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-aspectMask-07662) VUID-vkCmdCopyMemoryToImageIndirectNV-aspectMask-07662

The `aspectMask` member for every subresource in
`pImageSubresources` **must** only have a single bit set

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07663) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07663

The image region specified by each element in `copyBufferAddress`
**must** be a region that is contained within `dstImage`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07664) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07664

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07665) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07665

If `dstImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07973) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07973

`dstImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-07667) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-07667

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` at the time this command is executed on a
`VkDevice`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-07669) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-07669

`dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL`,
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
or `VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-mipLevel-07670) VUID-vkCmdCopyMemoryToImageIndirectNV-mipLevel-07670

The specified `mipLevel` of each region **must** be less than the
`mipLevels` specified in [VkImageCreateInfo](VkImageCreateInfo.html) when `dstImage`
was created

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-layerCount-08764) VUID-vkCmdCopyMemoryToImageIndirectNV-layerCount-08764

If `layerCount` is not `VK_REMAINING_ARRAY_LAYERS`, the
specified `baseArrayLayer` +  `layerCount` of each region
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](VkImageCreateInfo.html) when `dstImage` was created

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-imageOffset-07672) VUID-vkCmdCopyMemoryToImageIndirectNV-imageOffset-07672

The `imageOffset` and `imageExtent` members of each region **must**
respect the image transfer granularity requirements of
`commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](VkQueueFamilyProperties.html)

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07673) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07673

`dstImage` **must** not have been created with `flags` containing
`VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-07674) VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-07674

If the queue family used to create the [VkCommandPool](VkCommandPool.html) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each region, the `aspectMask`
member of `pImageSubresources` **must** not be
`VK_IMAGE_ASPECT_DEPTH_BIT` or `VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-imageOffset-07675) VUID-vkCmdCopyMemoryToImageIndirectNV-imageOffset-07675

For each region in `copyBufferAddress`, `imageOffset.y` and
(`imageExtent.height` +  `imageOffset.y`) **must** both
be greater than or equal to `0` and less than or equal to the height of
the specified subresource

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-offset-07676) VUID-vkCmdCopyMemoryToImageIndirectNV-offset-07676

`offset` **must** be 4 byte aligned

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-stride-07677) VUID-vkCmdCopyMemoryToImageIndirectNV-stride-07677

`stride` **must** be a multiple of `4` and **must** be greater than or
equal to sizeof(`VkCopyMemoryToImageIndirectCommandNV`)

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](VkCommandBuffer.html) handle

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-copyBufferAddress-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-copyBufferAddress-parameter

 `copyBufferAddress` **must** be a valid `VkDeviceAddress` value

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](VkImage.html) handle

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](VkImageLayout.html) value

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-pImageSubresources-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-pImageSubresources-parameter

 `pImageSubresources` **must** be a valid pointer to an array of `copyCount` valid [VkImageSubresourceLayers](VkImageSubresourceLayers.html) structures

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-recording) VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](../../../../spec/latest/chapters/cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-cmdpool) VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-renderpass) VUID-vkCmdCopyMemoryToImageIndirectNV-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-videocoding) VUID-vkCmdCopyMemoryToImageIndirectNV-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-copyCount-arraylength) VUID-vkCmdCopyMemoryToImageIndirectNV-copyCount-arraylength

 `copyCount` **must** be greater than `0`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-commonparent) VUID-vkCmdCopyMemoryToImageIndirectNV-commonparent

 Both of `commandBuffer`, and `dstImage` **must** have been created, allocated, or retrieved from the same [VkDevice](VkDevice.html)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties
| [Command Buffer Levels](../../../../spec/latest/chapters/cmdbuffers.html#VkCommandBufferLevel) | [Render Pass Scope](../../../../spec/latest/chapters/renderpass.html#vkCmdBeginRenderPass) | [Video Coding Scope](../../../../spec/latest/chapters/videocoding.html#vkCmdBeginVideoCodingKHR) | [Supported Queue Types](../../../../spec/latest/chapters/devsandqueues.html#VkQueueFlagBits) | [Command Type](../../../../spec/latest/chapters/fundamentals.html#fundamentals-queueoperation-command-types) |
| --- | --- | --- | --- | --- |
| Primary

Secondary | Outside | Outside | Transfer

Graphics

Compute | Action |

Conditional Rendering

vkCmdCopyMemoryToImageIndirectNV is not affected by [conditional rendering](../../../../spec/latest/chapters/drawing.html#drawing-conditional-rendering)

[VK_NV_copy_memory_indirect](VK_NV_copy_memory_indirect.html), [VkCommandBuffer](VkCommandBuffer.html), `VkDeviceAddress`, [VkImage](VkImage.html), [VkImageLayout](VkImageLayout.html), [VkImageSubresourceLayers](VkImageSubresourceLayers.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/copies.html#vkCmdCopyMemoryToImageIndirectNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
