# Copy Commands

## Metadata

- **Component**: spec
- **Version**: latest
- **URL**: /spec/latest/chapters/copies.html

## Table of Contents

- [Copying Data Between Buffers](#copies-buffers)
- [Copying_Data_Between_Buffers](#copies-buffers)
- [Copying Data Between Images](#copies-images)
- [Copying_Data_Between_Images](#copies-images)
- [Copying Data Between Buffers and Images](#copies-buffers-images)
- [Copying_Data_Between_Buffers_and_Images](#copies-buffers-images)
- [Indirect Copies](#indirect-copies)
- [Image Copies With Scaling](#copies-imagescaling)
- [Image_Copies_With_Scaling](#copies-imagescaling)
- [Image Blits With Scaling and Rotation](#copies-images-scaling-rotation)
- [Image_Blits_With_Scaling_and_Rotation](#copies-images-scaling-rotation)
- [Resolving Multisample Images](#copies-resolve)
- [Resolving_Multisample_Images](#copies-resolve)
- [Buffer Markers](#copies-buffer-markers)

## Content

An application **can** copy buffer and image data using several methods
described in this chapter, depending on the type of data transfer.

All copy commands are treated as “transfer” operations for the purposes of
synchronization barriers.

All copy commands that have a source format with an X component in its
format description read **undefined** values from those bits.

All copy commands that have a destination format with an X component in its
format description write **undefined** values to those bits.

To copy data between buffer objects, call:

// Provided by VK_VERSION_1_0
void vkCmdCopyBuffer(
    VkCommandBuffer                             commandBuffer,
    VkBuffer                                    srcBuffer,
    VkBuffer                                    dstBuffer,
    uint32_t                                    regionCount,
    const VkBufferCopy*                         pRegions);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`srcBuffer` is the source buffer.

* 
`dstBuffer` is the destination buffer.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkBufferCopy](#VkBufferCopy) structures
specifying the regions to copy.

Each source region specified by `pRegions` is copied from the source
buffer to the destination region of the destination buffer.
If any of the specified regions in `srcBuffer` overlaps in memory with
any of the specified regions in `dstBuffer`, values read from those
overlapping regions are **undefined**.

Valid Usage

* 
[](#VUID-vkCmdCopyBuffer-commandBuffer-01822) VUID-vkCmdCopyBuffer-commandBuffer-01822

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyBuffer-commandBuffer-01823) VUID-vkCmdCopyBuffer-commandBuffer-01823

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyBuffer-commandBuffer-01824) VUID-vkCmdCopyBuffer-commandBuffer-01824

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be an unprotected buffer

* 
[](#VUID-vkCmdCopyBuffer-srcOffset-00113) VUID-vkCmdCopyBuffer-srcOffset-00113

The `srcOffset` member of each element of `pRegions` **must** be
less than the size of `srcBuffer`

* 
[](#VUID-vkCmdCopyBuffer-dstOffset-00114) VUID-vkCmdCopyBuffer-dstOffset-00114

The `dstOffset` member of each element of `pRegions` **must** be
less than the size of `dstBuffer`

* 
[](#VUID-vkCmdCopyBuffer-size-00115) VUID-vkCmdCopyBuffer-size-00115

The `size` member of each element of `pRegions` **must** be less
than or equal to the size of `srcBuffer` minus `srcOffset`

* 
[](#VUID-vkCmdCopyBuffer-size-00116) VUID-vkCmdCopyBuffer-size-00116

The `size` member of each element of `pRegions` **must** be less
than or equal to the size of `dstBuffer` minus `dstOffset`

* 
[](#VUID-vkCmdCopyBuffer-pRegions-00117) VUID-vkCmdCopyBuffer-pRegions-00117

The union of the source regions, and the union of the destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-vkCmdCopyBuffer-srcBuffer-00118) VUID-vkCmdCopyBuffer-srcBuffer-00118

`srcBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-vkCmdCopyBuffer-srcBuffer-00119) VUID-vkCmdCopyBuffer-srcBuffer-00119

If `srcBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyBuffer-dstBuffer-00120) VUID-vkCmdCopyBuffer-dstBuffer-00120

`dstBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdCopyBuffer-dstBuffer-00121) VUID-vkCmdCopyBuffer-dstBuffer-00121

If `dstBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyBuffer-commandBuffer-parameter) VUID-vkCmdCopyBuffer-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyBuffer-srcBuffer-parameter) VUID-vkCmdCopyBuffer-srcBuffer-parameter

 `srcBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-vkCmdCopyBuffer-dstBuffer-parameter) VUID-vkCmdCopyBuffer-dstBuffer-parameter

 `dstBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-vkCmdCopyBuffer-pRegions-parameter) VUID-vkCmdCopyBuffer-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkBufferCopy](#VkBufferCopy) structures

* 
[](#VUID-vkCmdCopyBuffer-commandBuffer-recording) VUID-vkCmdCopyBuffer-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyBuffer-commandBuffer-cmdpool) VUID-vkCmdCopyBuffer-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyBuffer-renderpass) VUID-vkCmdCopyBuffer-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyBuffer-videocoding) VUID-vkCmdCopyBuffer-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdCopyBuffer-regionCount-arraylength) VUID-vkCmdCopyBuffer-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-vkCmdCopyBuffer-commonparent) VUID-vkCmdCopyBuffer-commonparent

 Each of `commandBuffer`, `dstBuffer`, and `srcBuffer` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The `VkBufferCopy` structure is defined as:

// Provided by VK_VERSION_1_0
typedef struct VkBufferCopy {
    VkDeviceSize    srcOffset;
    VkDeviceSize    dstOffset;
    VkDeviceSize    size;
} VkBufferCopy;

* 
`srcOffset` is the starting offset in bytes from the start of
`srcBuffer`.

* 
`dstOffset` is the starting offset in bytes from the start of
`dstBuffer`.

* 
`size` is the number of bytes to copy.

Valid Usage

* 
[](#VUID-VkBufferCopy-size-01988) VUID-VkBufferCopy-size-01988

The `size` **must** be greater than `0`

A more extensible version of the copy buffer command is defined below.

To copy data between buffer objects, call:

// Provided by VK_VERSION_1_3
void vkCmdCopyBuffer2(
    VkCommandBuffer                             commandBuffer,
    const VkCopyBufferInfo2*                    pCopyBufferInfo);

or the equivalent command

// Provided by VK_KHR_copy_commands2
void vkCmdCopyBuffer2KHR(
    VkCommandBuffer                             commandBuffer,
    const VkCopyBufferInfo2*                    pCopyBufferInfo);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`pCopyBufferInfo` is a pointer to a [VkCopyBufferInfo2](#VkCopyBufferInfo2)
structure describing the copy parameters.

Each source region specified by `pCopyBufferInfo->pRegions` is copied
from the source buffer to the destination region of the destination buffer.
If any of the specified regions in `pCopyBufferInfo->srcBuffer` overlaps
in memory with any of the specified regions in
`pCopyBufferInfo->dstBuffer`, values read from those overlapping regions
are **undefined**.

Valid Usage

* 
[](#VUID-vkCmdCopyBuffer2-commandBuffer-01822) VUID-vkCmdCopyBuffer2-commandBuffer-01822

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyBuffer2-commandBuffer-01823) VUID-vkCmdCopyBuffer2-commandBuffer-01823

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyBuffer2-commandBuffer-01824) VUID-vkCmdCopyBuffer2-commandBuffer-01824

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be an unprotected buffer

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyBuffer2-commandBuffer-parameter) VUID-vkCmdCopyBuffer2-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyBuffer2-pCopyBufferInfo-parameter) VUID-vkCmdCopyBuffer2-pCopyBufferInfo-parameter

 `pCopyBufferInfo` **must** be a valid pointer to a valid [VkCopyBufferInfo2](#VkCopyBufferInfo2) structure

* 
[](#VUID-vkCmdCopyBuffer2-commandBuffer-recording) VUID-vkCmdCopyBuffer2-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyBuffer2-commandBuffer-cmdpool) VUID-vkCmdCopyBuffer2-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyBuffer2-renderpass) VUID-vkCmdCopyBuffer2-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyBuffer2-videocoding) VUID-vkCmdCopyBuffer2-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The `VkCopyBufferInfo2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkCopyBufferInfo2 {
    VkStructureType         sType;
    const void*             pNext;
    VkBuffer                srcBuffer;
    VkBuffer                dstBuffer;
    uint32_t                regionCount;
    const VkBufferCopy2*    pRegions;
} VkCopyBufferInfo2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkCopyBufferInfo2 VkCopyBufferInfo2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcBuffer` is the source buffer.

* 
`dstBuffer` is the destination buffer.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkBufferCopy2](#VkBufferCopy2)
structures specifying the regions to copy.

Valid Usage

* 
[](#VUID-VkCopyBufferInfo2-srcOffset-00113) VUID-VkCopyBufferInfo2-srcOffset-00113

The `srcOffset` member of each element of `pRegions` **must** be
less than the size of `srcBuffer`

* 
[](#VUID-VkCopyBufferInfo2-dstOffset-00114) VUID-VkCopyBufferInfo2-dstOffset-00114

The `dstOffset` member of each element of `pRegions` **must** be
less than the size of `dstBuffer`

* 
[](#VUID-VkCopyBufferInfo2-size-00115) VUID-VkCopyBufferInfo2-size-00115

The `size` member of each element of `pRegions` **must** be less
than or equal to the size of `srcBuffer` minus `srcOffset`

* 
[](#VUID-VkCopyBufferInfo2-size-00116) VUID-VkCopyBufferInfo2-size-00116

The `size` member of each element of `pRegions` **must** be less
than or equal to the size of `dstBuffer` minus `dstOffset`

* 
[](#VUID-VkCopyBufferInfo2-pRegions-00117) VUID-VkCopyBufferInfo2-pRegions-00117

The union of the source regions, and the union of the destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-VkCopyBufferInfo2-srcBuffer-00118) VUID-VkCopyBufferInfo2-srcBuffer-00118

`srcBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-VkCopyBufferInfo2-srcBuffer-00119) VUID-VkCopyBufferInfo2-srcBuffer-00119

If `srcBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-VkCopyBufferInfo2-dstBuffer-00120) VUID-VkCopyBufferInfo2-dstBuffer-00120

`dstBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-VkCopyBufferInfo2-dstBuffer-00121) VUID-VkCopyBufferInfo2-dstBuffer-00121

If `dstBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

Valid Usage (Implicit)

* 
[](#VUID-VkCopyBufferInfo2-sType-sType) VUID-VkCopyBufferInfo2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_BUFFER_INFO_2`

* 
[](#VUID-VkCopyBufferInfo2-pNext-pNext) VUID-VkCopyBufferInfo2-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkCopyBufferInfo2-srcBuffer-parameter) VUID-VkCopyBufferInfo2-srcBuffer-parameter

 `srcBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-VkCopyBufferInfo2-dstBuffer-parameter) VUID-VkCopyBufferInfo2-dstBuffer-parameter

 `dstBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-VkCopyBufferInfo2-pRegions-parameter) VUID-VkCopyBufferInfo2-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkBufferCopy2](#VkBufferCopy2) structures

* 
[](#VUID-VkCopyBufferInfo2-regionCount-arraylength) VUID-VkCopyBufferInfo2-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkCopyBufferInfo2-commonparent) VUID-VkCopyBufferInfo2-commonparent

 Both of `dstBuffer`, and `srcBuffer` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

The `VkBufferCopy2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkBufferCopy2 {
    VkStructureType    sType;
    const void*        pNext;
    VkDeviceSize       srcOffset;
    VkDeviceSize       dstOffset;
    VkDeviceSize       size;
} VkBufferCopy2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkBufferCopy2 VkBufferCopy2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcOffset` is the starting offset in bytes from the start of
`srcBuffer`.

* 
`dstOffset` is the starting offset in bytes from the start of
`dstBuffer`.

* 
`size` is the number of bytes to copy.

Valid Usage

* 
[](#VUID-VkBufferCopy2-size-01988) VUID-VkBufferCopy2-size-01988

The `size` **must** be greater than `0`

Valid Usage (Implicit)

* 
[](#VUID-VkBufferCopy2-sType-sType) VUID-VkBufferCopy2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_BUFFER_COPY_2`

* 
[](#VUID-VkBufferCopy2-pNext-pNext) VUID-VkBufferCopy2-pNext-pNext

 `pNext` **must** be `NULL`

To copy data between image objects, call:

// Provided by VK_VERSION_1_0
void vkCmdCopyImage(
    VkCommandBuffer                             commandBuffer,
    VkImage                                     srcImage,
    VkImageLayout                               srcImageLayout,
    VkImage                                     dstImage,
    VkImageLayout                               dstImageLayout,
    uint32_t                                    regionCount,
    const VkImageCopy*                          pRegions);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the current layout of the source image
subresource.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the current layout of the destination image
subresource.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkImageCopy](#VkImageCopy) structures
specifying the regions to copy.

Each source region specified by `pRegions` is copied from the source
image to the destination region of the destination image.
If any of the specified regions in `srcImage` overlaps in memory with
any of the specified regions in `dstImage`, values read from those
overlapping regions are **undefined**.
If any region accesses a depth aspect in `dstImage`
and the `[VK_EXT_depth_range_unrestricted](../appendices/extensions.html#VK_EXT_depth_range_unrestricted)` extension is not enabled,
values copied from `srcBuffer` outside of the range [0,1] will be
written as **undefined** values to the destination image.

[Multi-planar images](formats.html#formats-multiplanar) **can** only be copied on a
per-plane basis, and the subresources used in each region when copying to or
from such images **must** specify only one plane, though different regions **can**
specify different planes.
When copying planes of multi-planar images, the format considered is the
[compatible format for that plane](formats.html#formats-compatible-planes), rather than
the format of the multi-planar image.

If the format of the destination image has a different
[block extent](formats.html#formats-compatibility-classes) than the source image (e.g.
one is a compressed format), the offset and extent for each of the regions
specified is [scaled according to the block extents of each format](formats.html#formats-size-compatibility) to match in size.
Copy regions for each image **must** be aligned to a multiple of the texel
block extent in each dimension, except at the edges of the image, where
region extents **must** match the edge of the image.

Image data **can** be copied between images with different image types.
If one image is `VK_IMAGE_TYPE_3D` and the other image is
`VK_IMAGE_TYPE_2D` with multiple layers, then each slice is copied to or
from a different layer; `depth` slices in the 3D image correspond to
`layerCount` layers in the 2D image, with an effective `depth` of
`1` used for the 2D image.
If the [`maintenance5`](features.html#features-maintenance5) feature is enabled, all
other combinations are allowed and function as if 1D images are 2D images
with a height of 1.
Otherwise, other combinations of image types are disallowed.

Valid Usage

* 
[](#VUID-vkCmdCopyImage-commandBuffer-01825) VUID-vkCmdCopyImage-commandBuffer-01825

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyImage-commandBuffer-01826) VUID-vkCmdCopyImage-commandBuffer-01826

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyImage-commandBuffer-01827) VUID-vkCmdCopyImage-commandBuffer-01827

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

* 
[](#VUID-vkCmdCopyImage-commandBuffer-10217) VUID-vkCmdCopyImage-commandBuffer-10217

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pRegions`, where
the `aspectMask` member of `srcSubresource` is
`VK_IMAGE_ASPECT_COLOR_BIT`, the `aspectMask` of
`dstSubresource` **must** not be `VK_IMAGE_ASPECT_DEPTH_BIT` or
`VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyImage-commandBuffer-10218) VUID-vkCmdCopyImage-commandBuffer-10218

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pRegions`, where
the `aspectMask` member of `dstSubresource` is
`VK_IMAGE_ASPECT_COLOR_BIT` then the `aspectMask` of
`srcSubresource` **must** not be `VK_IMAGE_ASPECT_DEPTH_BIT` or
`VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyImage-pRegions-00124) VUID-vkCmdCopyImage-pRegions-00124

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-vkCmdCopyImage-srcImage-01995) VUID-vkCmdCopyImage-srcImage-01995

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_SRC_BIT`

* 
[](#VUID-vkCmdCopyImage-srcImageLayout-00128) VUID-vkCmdCopyImage-srcImageLayout-00128

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdCopyImage-srcImageLayout-01917) VUID-vkCmdCopyImage-srcImageLayout-01917

`srcImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdCopyImage-srcImage-09460) VUID-vkCmdCopyImage-srcImage-09460

If `srcImage` and `dstImage` are the same, and any elements of
`pRegions` contains the `srcSubresource` and
`dstSubresource` with matching `mipLevel` and overlapping array
layers, then the `srcImageLayout` and `dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_GENERAL`
or `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`

* 
[](#VUID-vkCmdCopyImage-dstImage-01996) VUID-vkCmdCopyImage-dstImage-01996

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_DST_BIT`

* 
[](#VUID-vkCmdCopyImage-dstImageLayout-00133) VUID-vkCmdCopyImage-dstImageLayout-00133

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdCopyImage-dstImageLayout-01395) VUID-vkCmdCopyImage-dstImageLayout-01395

`dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdCopyImage-srcImage-01548) VUID-vkCmdCopyImage-srcImage-01548

If the [VkFormat](formats.html#VkFormat) of each of `srcImage` and `dstImage` is
not a [multi-planar format](formats.html#formats-multiplanar), the
[VkFormat](formats.html#VkFormat) of each of `srcImage` and `dstImage` **must** be
[size-compatible](formats.html#formats-size-compatibility)

* 
[](#VUID-vkCmdCopyImage-None-01549) VUID-vkCmdCopyImage-None-01549

 In a copy to or from a plane of a
[multi-planar image](formats.html#formats-multiplanar), the [VkFormat](formats.html#VkFormat) of the
 image and plane **must** be compatible according to
 [the description of compatible planes](formats.html#formats-compatible-planes) for
 the plane being copied

* 
[](#VUID-vkCmdCopyImage-srcImage-09247) VUID-vkCmdCopyImage-srcImage-09247

If the [VkFormat](formats.html#VkFormat) of each of `srcImage` and `dstImage` is a
[compressed image format](../appendices/compressedtex.html#compressed_image_formats), the formats **must**
have the same texel block extent

* 
[](#VUID-vkCmdCopyImage-srcImage-00136) VUID-vkCmdCopyImage-srcImage-00136

The sample count of `srcImage` and `dstImage` **must** match

* 
[](#VUID-vkCmdCopyImage-srcOffset-01783) VUID-vkCmdCopyImage-srcOffset-01783

The `srcOffset` and `extent` members of each element of
`pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-vkCmdCopyImage-dstOffset-01784) VUID-vkCmdCopyImage-dstOffset-01784

The `dstOffset` and `extent` members of each element of
`pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-vkCmdCopyImage-srcImage-01551) VUID-vkCmdCopyImage-srcImage-01551

    If neither `srcImage` nor `dstImage` has a
    [multi-planar format](formats.html#formats-multiplanar)
and the [`maintenance8`](features.html#features-maintenance8) feature is not enabled
    then for each element of `pRegions`, `srcSubresource.aspectMask`
    and `dstSubresource.aspectMask` **must** match

* 
[](#VUID-vkCmdCopyImage-srcSubresource-10214) VUID-vkCmdCopyImage-srcSubresource-10214

If `srcSubresource.aspectMask` is `VK_IMAGE_ASPECT_COLOR_BIT`,
then `dstSubresource.aspectMask` **must** not contain both
`VK_IMAGE_ASPECT_DEPTH_BIT` and `VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyImage-dstSubresource-10215) VUID-vkCmdCopyImage-dstSubresource-10215

If `dstSubresource.aspectMask` is `VK_IMAGE_ASPECT_COLOR_BIT`,
then `srSubresource.aspectMask` **must** not contain both
`VK_IMAGE_ASPECT_DEPTH_BIT` and `VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyImage-srcImage-08713) VUID-vkCmdCopyImage-srcImage-08713

If `srcImage` has a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `srcSubresource.aspectMask`
**must** be a single valid [multi-planar    aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-vkCmdCopyImage-dstImage-08714) VUID-vkCmdCopyImage-dstImage-08714

If `dstImage` has a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `dstSubresource.aspectMask`
**must** be a single valid [multi-planar    aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-vkCmdCopyImage-srcImage-01556) VUID-vkCmdCopyImage-srcImage-01556

If `srcImage` has a [multi-planar format](formats.html#formats-multiplanar) and
the `dstImage` does not have a multi-planar image format, then for
each element of `pRegions`, `dstSubresource.aspectMask` **must** be
`VK_IMAGE_ASPECT_COLOR_BIT`

* 
[](#VUID-vkCmdCopyImage-dstImage-01557) VUID-vkCmdCopyImage-dstImage-01557

If `dstImage` has a [multi-planar format](formats.html#formats-multiplanar) and
the `srcImage` does not have a multi-planar image format, then for
each element of `pRegions`, `srcSubresource.aspectMask` **must** be
`VK_IMAGE_ASPECT_COLOR_BIT`

* 
[](#VUID-vkCmdCopyImage-srcSubresource-10211) VUID-vkCmdCopyImage-srcSubresource-10211

If `srcSubresource.aspectMask` is `VK_IMAGE_ASPECT_COLOR_BIT`
and `dstSubresource.aspectMask` is `VK_IMAGE_ASPECT_DEPTH_BIT`
or `VK_IMAGE_ASPECT_STENCIL_BIT`, then the [VkFormat](formats.html#VkFormat) values of
`srcImage` and `dstImage` **must** be compatible according to
[the list of compatible depth-stencil and    color formats](formats.html#formats-compatible-zs-color)

* 
[](#VUID-vkCmdCopyImage-srcSubresource-10212) VUID-vkCmdCopyImage-srcSubresource-10212

If `srcSubresource.aspectMask` is `VK_IMAGE_ASPECT_DEPTH_BIT` or
`VK_IMAGE_ASPECT_STENCIL_BIT` and `dstSubresource.aspectMask` is
`VK_IMAGE_ASPECT_COLOR_BIT`, then the [VkFormat](formats.html#VkFormat) values of
`srcImage` and `dstImage` **must** be compatible according to
[the list of compatible depth-stencil and    color formats](formats.html#formats-compatible-zs-color)

* 
[](#VUID-vkCmdCopyImage-apiVersion-07932) VUID-vkCmdCopyImage-apiVersion-07932

    If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
or
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
and
    either `srcImage` or `dstImage` is of type
    `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
    `srcSubresource.baseArrayLayer` and
    `dstSubresource.baseArrayLayer` **must** both be `0`, and
    `srcSubresource.layerCount` and `dstSubresource.layerCount`
    **must** both be `1`

* 
[](#VUID-vkCmdCopyImage-srcImage-04443) VUID-vkCmdCopyImage-srcImage-04443

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcSubresource.baseArrayLayer` **must** be
`0` and `srcSubresource.layerCount` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-dstImage-04444) VUID-vkCmdCopyImage-dstImage-04444

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstSubresource.baseArrayLayer` **must** be
`0` and `dstSubresource.layerCount` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-aspectMask-00142) VUID-vkCmdCopyImage-aspectMask-00142

For each element of `pRegions`, `srcSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-vkCmdCopyImage-aspectMask-00143) VUID-vkCmdCopyImage-aspectMask-00143

For each element of `pRegions`, `dstSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-vkCmdCopyImage-srcOffset-00144) VUID-vkCmdCopyImage-srcOffset-00144

For each element of `pRegions`, `srcOffset.x` and
(`extent.width` +  `srcOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-vkCmdCopyImage-srcOffset-00145) VUID-vkCmdCopyImage-srcOffset-00145

For each element of `pRegions`, `srcOffset.y` and
(`extent.height` +  `srcOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-vkCmdCopyImage-srcImage-00146) VUID-vkCmdCopyImage-srcImage-00146

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-srcOffset-00147) VUID-vkCmdCopyImage-srcOffset-00147

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcOffset.z` and
(`extent.depth` +  `srcOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-vkCmdCopyImage-srcImage-01785) VUID-vkCmdCopyImage-srcImage-01785

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffset.z` **must** be `0` and
`extent.depth` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-dstImage-01786) VUID-vkCmdCopyImage-dstImage-01786

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffset.z` **must** be `0` and
`extent.depth` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-srcImage-01787) VUID-vkCmdCopyImage-srcImage-01787

If `srcImage` is of type `VK_IMAGE_TYPE_2D`, then for each
element of `pRegions`, `srcOffset.z` **must** be `0`

* 
[](#VUID-vkCmdCopyImage-dstImage-01788) VUID-vkCmdCopyImage-dstImage-01788

If `dstImage` is of type `VK_IMAGE_TYPE_2D`, then for each
element of `pRegions`, `dstOffset.z` **must** be `0`

* 
[](#VUID-vkCmdCopyImage-apiVersion-07933) VUID-vkCmdCopyImage-apiVersion-07933

    If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
    `srcImage` and `dstImage` **must** have the same [VkImageType](resources.html#VkImageType)

* 
[](#VUID-vkCmdCopyImage-apiVersion-08969) VUID-vkCmdCopyImage-apiVersion-08969

    If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
    `srcImage` or `dstImage` is of type `VK_IMAGE_TYPE_2D`, then
    for each element of `pRegions`, `extent.depth` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-srcImage-07743) VUID-vkCmdCopyImage-srcImage-07743

If `srcImage` and `dstImage` have a different [VkImageType](resources.html#VkImageType),
and the [`maintenance5`](features.html#features-maintenance5) feature is not
enabled,
one **must** be `VK_IMAGE_TYPE_3D` and the other **must** be
`VK_IMAGE_TYPE_2D`

* 
[](#VUID-vkCmdCopyImage-srcImage-08793) VUID-vkCmdCopyImage-srcImage-08793

If `srcImage` and `dstImage` have the same [VkImageType](resources.html#VkImageType),
for each element of `pRegions`,
if neither of the `layerCount` members of `srcSubresource` or
`dstSubresource` are `VK_REMAINING_ARRAY_LAYERS`,
the `layerCount` members of `srcSubresource` or
`dstSubresource` **must** match

* 
[](#VUID-vkCmdCopyImage-srcImage-08794) VUID-vkCmdCopyImage-srcImage-08794

If `srcImage` and `dstImage` have the same [VkImageType](resources.html#VkImageType),
and one of the `layerCount` members of `srcSubresource` or
`dstSubresource` is `VK_REMAINING_ARRAY_LAYERS`, the other
member **must** be either `VK_REMAINING_ARRAY_LAYERS` or equal to the
`arrayLayers` member of the [VkImageCreateInfo](resources.html#VkImageCreateInfo) used to create
the image minus `baseArrayLayer`

* 
[](#VUID-vkCmdCopyImage-srcImage-01790) VUID-vkCmdCopyImage-srcImage-01790

If `srcImage` and `dstImage` are both of type
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`extent.depth` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-srcImage-01791) VUID-vkCmdCopyImage-srcImage-01791

If `srcImage` is of type `VK_IMAGE_TYPE_2D`, and `dstImage`
is of type `VK_IMAGE_TYPE_3D`, then for each element of
`pRegions`, `extent.depth` **must** equal
`srcSubresource.layerCount`

* 
[](#VUID-vkCmdCopyImage-dstImage-01792) VUID-vkCmdCopyImage-dstImage-01792

If `dstImage` is of type `VK_IMAGE_TYPE_2D`, and `srcImage`
is of type `VK_IMAGE_TYPE_3D`, then for each element of
`pRegions`, `extent.depth` **must** equal
`dstSubresource.layerCount`

* 
[](#VUID-vkCmdCopyImage-dstOffset-00150) VUID-vkCmdCopyImage-dstOffset-00150

For each element of `pRegions`, `dstOffset.x` and
(`extent.width` +  `dstOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-vkCmdCopyImage-dstOffset-00151) VUID-vkCmdCopyImage-dstOffset-00151

For each element of `pRegions`, `dstOffset.y` and
(`extent.height` +  `dstOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-vkCmdCopyImage-dstImage-00152) VUID-vkCmdCopyImage-dstImage-00152

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-vkCmdCopyImage-dstOffset-00153) VUID-vkCmdCopyImage-dstOffset-00153

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstOffset.z` and
(`extent.depth` +  `dstOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-vkCmdCopyImage-pRegions-07278) VUID-vkCmdCopyImage-pRegions-07278

For each element of `pRegions`, `srcOffset.x` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImage-pRegions-07279) VUID-vkCmdCopyImage-pRegions-07279

For each element of `pRegions`, `srcOffset.y` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImage-pRegions-07280) VUID-vkCmdCopyImage-pRegions-07280

For each element of `pRegions`, `srcOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImage-pRegions-07281) VUID-vkCmdCopyImage-pRegions-07281

For each element of `pRegions`, `dstOffset.x` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyImage-pRegions-07282) VUID-vkCmdCopyImage-pRegions-07282

For each element of `pRegions`, `dstOffset.y` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyImage-pRegions-07283) VUID-vkCmdCopyImage-pRegions-07283

For each element of `pRegions`, `dstOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyImage-srcImage-01728) VUID-vkCmdCopyImage-srcImage-01728

For each element of `pRegions`, if the sum of `srcOffset.x` and
`extent.width` does not equal the width of the subresource specified
by `srcSubresource`, `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImage-srcImage-01729) VUID-vkCmdCopyImage-srcImage-01729

For each element of `pRegions`, if the sum of `srcOffset.y` and
`extent.height` does not equal the height of the subresource
specified by `srcSubresource`, `extent.height` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImage-srcImage-01730) VUID-vkCmdCopyImage-srcImage-01730

For each element of `pRegions`, if the sum of `srcOffset.z` and
`extent.depth` does not equal the depth of the subresource specified
by `srcSubresource`, `extent.depth` **must** be a multiple of the
[texel block extent depth](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImage-dstImage-01732) VUID-vkCmdCopyImage-dstImage-01732

For each element of `pRegions`, if the sum of `dstOffset.x` and
`extent.width` does not equal the width of the subresource specified
by `dstSubresource`, `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyImage-dstImage-01733) VUID-vkCmdCopyImage-dstImage-01733

For each element of `pRegions`, if the sum of `dstOffset.y` and
`extent.height` does not equal the height of the subresource
specified by `dstSubresource`, `extent.height` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyImage-dstImage-01734) VUID-vkCmdCopyImage-dstImage-01734

For each element of `pRegions`, if the sum of `dstOffset.z` and
`extent.depth` does not equal the depth of the subresource specified
by `dstSubresource`, `extent.depth` **must** be a multiple of the
[texel block extent depth](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyImage-aspect-06662) VUID-vkCmdCopyImage-aspect-06662

If the `aspect` member of any element of `pRegions` includes any
flag other than `VK_IMAGE_ASPECT_STENCIL_BIT` or `srcImage` was
not created with [separate stencil    usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` **must** have been included in the
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage` used to create `srcImage`

* 
[](#VUID-vkCmdCopyImage-aspect-06663) VUID-vkCmdCopyImage-aspect-06663

If the `aspect` member of any element of `pRegions` includes any
flag other than `VK_IMAGE_ASPECT_STENCIL_BIT` or `dstImage` was
not created with [separate stencil    usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` **must** have been included in the
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage` used to create `dstImage`

* 
[](#VUID-vkCmdCopyImage-aspect-06664) VUID-vkCmdCopyImage-aspect-06664

If the `aspect` member of any element of `pRegions` includes
`VK_IMAGE_ASPECT_STENCIL_BIT`, and `srcImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` **must** have been included in the
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage` used to create
`srcImage`

* 
[](#VUID-vkCmdCopyImage-aspect-06665) VUID-vkCmdCopyImage-aspect-06665

If the `aspect` member of any element of `pRegions` includes
`VK_IMAGE_ASPECT_STENCIL_BIT`, and `dstImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` **must** have been included in the
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage` used to create
`dstImage`

* 
[](#VUID-vkCmdCopyImage-srcImage-07966) VUID-vkCmdCopyImage-srcImage-07966

If `srcImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyImage-srcSubresource-07967) VUID-vkCmdCopyImage-srcSubresource-07967

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdCopyImage-srcSubresource-07968) VUID-vkCmdCopyImage-srcSubresource-07968

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdCopyImage-srcImage-07969) VUID-vkCmdCopyImage-srcImage-07969

`srcImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-vkCmdCopyImage-dstImage-07966) VUID-vkCmdCopyImage-dstImage-07966

If `dstImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyImage-dstSubresource-07967) VUID-vkCmdCopyImage-dstSubresource-07967

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdCopyImage-dstSubresource-07968) VUID-vkCmdCopyImage-dstSubresource-07968

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdCopyImage-dstImage-07969) VUID-vkCmdCopyImage-dstImage-07969

`dstImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyImage-commandBuffer-parameter) VUID-vkCmdCopyImage-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyImage-srcImage-parameter) VUID-vkCmdCopyImage-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdCopyImage-srcImageLayout-parameter) VUID-vkCmdCopyImage-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdCopyImage-dstImage-parameter) VUID-vkCmdCopyImage-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdCopyImage-dstImageLayout-parameter) VUID-vkCmdCopyImage-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdCopyImage-pRegions-parameter) VUID-vkCmdCopyImage-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageCopy](#VkImageCopy) structures

* 
[](#VUID-vkCmdCopyImage-commandBuffer-recording) VUID-vkCmdCopyImage-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyImage-commandBuffer-cmdpool) VUID-vkCmdCopyImage-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyImage-renderpass) VUID-vkCmdCopyImage-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyImage-videocoding) VUID-vkCmdCopyImage-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdCopyImage-regionCount-arraylength) VUID-vkCmdCopyImage-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-vkCmdCopyImage-commonparent) VUID-vkCmdCopyImage-commonparent

 Each of `commandBuffer`, `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The `VkImageCopy` structure is defined as:

// Provided by VK_VERSION_1_0
typedef struct VkImageCopy {
    VkImageSubresourceLayers    srcSubresource;
    VkOffset3D                  srcOffset;
    VkImageSubresourceLayers    dstSubresource;
    VkOffset3D                  dstOffset;
    VkExtent3D                  extent;
} VkImageCopy;

* 
`srcSubresource` and `dstSubresource` are
[VkImageSubresourceLayers](#VkImageSubresourceLayers) structures specifying the image
subresources of the images used for the source and destination image
data, respectively.

* 
`srcOffset` and `dstOffset` select the initial `x`, `y`,
and `z` offsets in texels of the sub-regions of the source and
destination image data.

* 
`extent` is the size in texels of the image to copy in `width`,
`height` and `depth`.

Valid Usage

* 
[](#VUID-VkImageCopy-apiVersion-07940) VUID-VkImageCopy-apiVersion-07940

If
    the [VK_KHR_sampler_ycbcr_conversion](../appendices/extensions.html#VK_KHR_sampler_ycbcr_conversion) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
the
    `aspectMask` member of `srcSubresource` and `dstSubresource`
    **must** match

* 
[](#VUID-VkImageCopy-apiVersion-07941) VUID-VkImageCopy-apiVersion-07941

If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
the
    `layerCount` member of `srcSubresource` and `dstSubresource`
    **must** match

* 
[](#VUID-VkImageCopy-extent-06668) VUID-VkImageCopy-extent-06668

`extent.width` **must** not be 0

* 
[](#VUID-VkImageCopy-extent-06669) VUID-VkImageCopy-extent-06669

`extent.height` **must** not be 0

* 
[](#VUID-VkImageCopy-extent-06670) VUID-VkImageCopy-extent-06670

`extent.depth` **must** not be 0

Valid Usage (Implicit)

* 
[](#VUID-VkImageCopy-srcSubresource-parameter) VUID-VkImageCopy-srcSubresource-parameter

 `srcSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

* 
[](#VUID-VkImageCopy-dstSubresource-parameter) VUID-VkImageCopy-dstSubresource-parameter

 `dstSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

The `VkImageSubresourceLayers` structure is defined as:

// Provided by VK_VERSION_1_0
typedef struct VkImageSubresourceLayers {
    VkImageAspectFlags    aspectMask;
    uint32_t              mipLevel;
    uint32_t              baseArrayLayer;
    uint32_t              layerCount;
} VkImageSubresourceLayers;

* 
`aspectMask` is a combination of [VkImageAspectFlagBits](resources.html#VkImageAspectFlagBits),
selecting the color, depth and/or stencil aspects to be copied.

* 
`mipLevel` is the mipmap level to copy

* 
`baseArrayLayer` and `layerCount` are the starting layer and
number of layers to copy.

Valid Usage

* 
[](#VUID-VkImageSubresourceLayers-aspectMask-00167) VUID-VkImageSubresourceLayers-aspectMask-00167

If `aspectMask` contains `VK_IMAGE_ASPECT_COLOR_BIT`, it **must**
not contain either of `VK_IMAGE_ASPECT_DEPTH_BIT` or
`VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-VkImageSubresourceLayers-aspectMask-00168) VUID-VkImageSubresourceLayers-aspectMask-00168

`aspectMask` **must** not contain `VK_IMAGE_ASPECT_METADATA_BIT`

* 
[](#VUID-VkImageSubresourceLayers-aspectMask-02247) VUID-VkImageSubresourceLayers-aspectMask-02247

`aspectMask` **must** not include
`VK_IMAGE_ASPECT_MEMORY_PLANE*_i_*BIT_EXT` for any index *i*

* 
[](#VUID-VkImageSubresourceLayers-layerCount-09243) VUID-VkImageSubresourceLayers-layerCount-09243

If the [`maintenance5`](features.html#features-maintenance5) feature is not
enabled,
`layerCount` **must** not be `VK_REMAINING_ARRAY_LAYERS`

* 
[](#VUID-VkImageSubresourceLayers-layerCount-01700) VUID-VkImageSubresourceLayers-layerCount-01700

If `layerCount` is not `VK_REMAINING_ARRAY_LAYERS`, it **must** be
greater than 0

Valid Usage (Implicit)

* 
[](#VUID-VkImageSubresourceLayers-aspectMask-parameter) VUID-VkImageSubresourceLayers-aspectMask-parameter

 `aspectMask` **must** be a valid combination of [VkImageAspectFlagBits](resources.html#VkImageAspectFlagBits) values

* 
[](#VUID-VkImageSubresourceLayers-aspectMask-requiredbitmask) VUID-VkImageSubresourceLayers-aspectMask-requiredbitmask

 `aspectMask` **must** not be `0`

A more extensible version of the copy image command is defined below.

To copy data between image objects, call:

// Provided by VK_VERSION_1_3
void vkCmdCopyImage2(
    VkCommandBuffer                             commandBuffer,
    const VkCopyImageInfo2*                     pCopyImageInfo);

or the equivalent command

// Provided by VK_KHR_copy_commands2
void vkCmdCopyImage2KHR(
    VkCommandBuffer                             commandBuffer,
    const VkCopyImageInfo2*                     pCopyImageInfo);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`pCopyImageInfo` is a pointer to a [VkCopyImageInfo2](#VkCopyImageInfo2) structure
describing the copy parameters.

This command is functionally identical to [vkCmdCopyImage](#vkCmdCopyImage), but includes
extensible sub-structures that include `sType` and `pNext`
parameters, allowing them to be more easily extended.

Valid Usage

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-01825) VUID-vkCmdCopyImage2-commandBuffer-01825

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-01826) VUID-vkCmdCopyImage2-commandBuffer-01826

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-01827) VUID-vkCmdCopyImage2-commandBuffer-01827

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-10217) VUID-vkCmdCopyImage2-commandBuffer-10217

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pCopyImageInfo->pRegions`, where
the `aspectMask` member of `srcSubresource` is
`VK_IMAGE_ASPECT_COLOR_BIT`, the `aspectMask` of
`dstSubresource` **must** not be `VK_IMAGE_ASPECT_DEPTH_BIT` or
`VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-10218) VUID-vkCmdCopyImage2-commandBuffer-10218

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pCopyImageInfo->pRegions`, where
the `aspectMask` member of `dstSubresource` is
`VK_IMAGE_ASPECT_COLOR_BIT` then the `aspectMask` of
`srcSubresource` **must** not be `VK_IMAGE_ASPECT_DEPTH_BIT` or
`VK_IMAGE_ASPECT_STENCIL_BIT`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-parameter) VUID-vkCmdCopyImage2-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyImage2-pCopyImageInfo-parameter) VUID-vkCmdCopyImage2-pCopyImageInfo-parameter

 `pCopyImageInfo` **must** be a valid pointer to a valid [VkCopyImageInfo2](#VkCopyImageInfo2) structure

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-recording) VUID-vkCmdCopyImage2-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyImage2-commandBuffer-cmdpool) VUID-vkCmdCopyImage2-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyImage2-renderpass) VUID-vkCmdCopyImage2-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyImage2-videocoding) VUID-vkCmdCopyImage2-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The `VkCopyImageInfo2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkCopyImageInfo2 {
    VkStructureType        sType;
    const void*            pNext;
    VkImage                srcImage;
    VkImageLayout          srcImageLayout;
    VkImage                dstImage;
    VkImageLayout          dstImageLayout;
    uint32_t               regionCount;
    const VkImageCopy2*    pRegions;
} VkCopyImageInfo2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkCopyImageInfo2 VkCopyImageInfo2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the current layout of the source image
subresource.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the current layout of the destination image
subresource.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkImageCopy2](#VkImageCopy2) structures
specifying the regions to copy.

Valid Usage

* 
[](#VUID-VkCopyImageInfo2-pRegions-00124) VUID-VkCopyImageInfo2-pRegions-00124

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-VkCopyImageInfo2-srcImage-01995) VUID-VkCopyImageInfo2-srcImage-01995

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_SRC_BIT`

* 
[](#VUID-VkCopyImageInfo2-srcImageLayout-00128) VUID-VkCopyImageInfo2-srcImageLayout-00128

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkCopyImageInfo2-srcImageLayout-01917) VUID-VkCopyImageInfo2-srcImageLayout-01917

`srcImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkCopyImageInfo2-srcImage-09460) VUID-VkCopyImageInfo2-srcImage-09460

If `srcImage` and `dstImage` are the same, and any elements of
`pRegions` contains the `srcSubresource` and
`dstSubresource` with matching `mipLevel` and overlapping array
layers, then the `srcImageLayout` and `dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_GENERAL`
or `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01996) VUID-VkCopyImageInfo2-dstImage-01996

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_DST_BIT`

* 
[](#VUID-VkCopyImageInfo2-dstImageLayout-00133) VUID-VkCopyImageInfo2-dstImageLayout-00133

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkCopyImageInfo2-dstImageLayout-01395) VUID-VkCopyImageInfo2-dstImageLayout-01395

`dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01548) VUID-VkCopyImageInfo2-srcImage-01548

If the [VkFormat](formats.html#VkFormat) of each of `srcImage` and `dstImage` is
not a [multi-planar format](formats.html#formats-multiplanar), the
[VkFormat](formats.html#VkFormat) of each of `srcImage` and `dstImage` **must** be
[size-compatible](formats.html#formats-size-compatibility)

* 
[](#VUID-VkCopyImageInfo2-None-01549) VUID-VkCopyImageInfo2-None-01549

 In a copy to or from a plane of a
[multi-planar image](formats.html#formats-multiplanar), the [VkFormat](formats.html#VkFormat) of the
 image and plane **must** be compatible according to
 [the description of compatible planes](formats.html#formats-compatible-planes) for
 the plane being copied

* 
[](#VUID-VkCopyImageInfo2-srcImage-09247) VUID-VkCopyImageInfo2-srcImage-09247

If the [VkFormat](formats.html#VkFormat) of each of `srcImage` and `dstImage` is a
[compressed image format](../appendices/compressedtex.html#compressed_image_formats), the formats **must**
have the same texel block extent

* 
[](#VUID-VkCopyImageInfo2-srcImage-00136) VUID-VkCopyImageInfo2-srcImage-00136

The sample count of `srcImage` and `dstImage` **must** match

* 
[](#VUID-VkCopyImageInfo2-srcOffset-01783) VUID-VkCopyImageInfo2-srcOffset-01783

The `srcOffset` and `extent` members of each element of
`pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-VkCopyImageInfo2-dstOffset-01784) VUID-VkCopyImageInfo2-dstOffset-01784

The `dstOffset` and `extent` members of each element of
`pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-VkCopyImageInfo2-srcImage-01551) VUID-VkCopyImageInfo2-srcImage-01551

    If neither `srcImage` nor `dstImage` has a
    [multi-planar format](formats.html#formats-multiplanar)
and the [`maintenance8`](features.html#features-maintenance8) feature is not enabled
    then for each element of `pRegions`, `srcSubresource.aspectMask`
    and `dstSubresource.aspectMask` **must** match

* 
[](#VUID-VkCopyImageInfo2-srcSubresource-10214) VUID-VkCopyImageInfo2-srcSubresource-10214

If `srcSubresource.aspectMask` is `VK_IMAGE_ASPECT_COLOR_BIT`,
then `dstSubresource.aspectMask` **must** not contain both
`VK_IMAGE_ASPECT_DEPTH_BIT` and `VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-VkCopyImageInfo2-dstSubresource-10215) VUID-VkCopyImageInfo2-dstSubresource-10215

If `dstSubresource.aspectMask` is `VK_IMAGE_ASPECT_COLOR_BIT`,
then `srSubresource.aspectMask` **must** not contain both
`VK_IMAGE_ASPECT_DEPTH_BIT` and `VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-VkCopyImageInfo2-srcImage-08713) VUID-VkCopyImageInfo2-srcImage-08713

If `srcImage` has a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `srcSubresource.aspectMask`
**must** be a single valid [multi-planar    aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyImageInfo2-dstImage-08714) VUID-VkCopyImageInfo2-dstImage-08714

If `dstImage` has a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `dstSubresource.aspectMask`
**must** be a single valid [multi-planar    aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyImageInfo2-srcImage-01556) VUID-VkCopyImageInfo2-srcImage-01556

If `srcImage` has a [multi-planar format](formats.html#formats-multiplanar) and
the `dstImage` does not have a multi-planar image format, then for
each element of `pRegions`, `dstSubresource.aspectMask` **must** be
`VK_IMAGE_ASPECT_COLOR_BIT`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01557) VUID-VkCopyImageInfo2-dstImage-01557

If `dstImage` has a [multi-planar format](formats.html#formats-multiplanar) and
the `srcImage` does not have a multi-planar image format, then for
each element of `pRegions`, `srcSubresource.aspectMask` **must** be
`VK_IMAGE_ASPECT_COLOR_BIT`

* 
[](#VUID-VkCopyImageInfo2-srcSubresource-10211) VUID-VkCopyImageInfo2-srcSubresource-10211

If `srcSubresource.aspectMask` is `VK_IMAGE_ASPECT_COLOR_BIT`
and `dstSubresource.aspectMask` is `VK_IMAGE_ASPECT_DEPTH_BIT`
or `VK_IMAGE_ASPECT_STENCIL_BIT`, then the [VkFormat](formats.html#VkFormat) values of
`srcImage` and `dstImage` **must** be compatible according to
[the list of compatible depth-stencil and    color formats](formats.html#formats-compatible-zs-color)

* 
[](#VUID-VkCopyImageInfo2-srcSubresource-10212) VUID-VkCopyImageInfo2-srcSubresource-10212

If `srcSubresource.aspectMask` is `VK_IMAGE_ASPECT_DEPTH_BIT` or
`VK_IMAGE_ASPECT_STENCIL_BIT` and `dstSubresource.aspectMask` is
`VK_IMAGE_ASPECT_COLOR_BIT`, then the [VkFormat](formats.html#VkFormat) values of
`srcImage` and `dstImage` **must** be compatible according to
[the list of compatible depth-stencil and    color formats](formats.html#formats-compatible-zs-color)

* 
[](#VUID-VkCopyImageInfo2-apiVersion-07932) VUID-VkCopyImageInfo2-apiVersion-07932

    If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
or
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
and
    either `srcImage` or `dstImage` is of type
    `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
    `srcSubresource.baseArrayLayer` and
    `dstSubresource.baseArrayLayer` **must** both be `0`, and
    `srcSubresource.layerCount` and `dstSubresource.layerCount`
    **must** both be `1`

* 
[](#VUID-VkCopyImageInfo2-srcImage-04443) VUID-VkCopyImageInfo2-srcImage-04443

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcSubresource.baseArrayLayer` **must** be
`0` and `srcSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-dstImage-04444) VUID-VkCopyImageInfo2-dstImage-04444

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstSubresource.baseArrayLayer` **must** be
`0` and `dstSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-aspectMask-00142) VUID-VkCopyImageInfo2-aspectMask-00142

For each element of `pRegions`, `srcSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-VkCopyImageInfo2-aspectMask-00143) VUID-VkCopyImageInfo2-aspectMask-00143

For each element of `pRegions`, `dstSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-VkCopyImageInfo2-srcOffset-00144) VUID-VkCopyImageInfo2-srcOffset-00144

For each element of `pRegions`, `srcOffset.x` and
(`extent.width` +  `srcOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-srcOffset-00145) VUID-VkCopyImageInfo2-srcOffset-00145

For each element of `pRegions`, `srcOffset.y` and
(`extent.height` +  `srcOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-srcImage-00146) VUID-VkCopyImageInfo2-srcImage-00146

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-srcOffset-00147) VUID-VkCopyImageInfo2-srcOffset-00147

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcOffset.z` and
(`extent.depth` +  `srcOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01785) VUID-VkCopyImageInfo2-srcImage-01785

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffset.z` **must** be `0` and
`extent.depth` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01786) VUID-VkCopyImageInfo2-dstImage-01786

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffset.z` **must** be `0` and
`extent.depth` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01787) VUID-VkCopyImageInfo2-srcImage-01787

If `srcImage` is of type `VK_IMAGE_TYPE_2D`, then for each
element of `pRegions`, `srcOffset.z` **must** be `0`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01788) VUID-VkCopyImageInfo2-dstImage-01788

If `dstImage` is of type `VK_IMAGE_TYPE_2D`, then for each
element of `pRegions`, `dstOffset.z` **must** be `0`

* 
[](#VUID-VkCopyImageInfo2-apiVersion-07933) VUID-VkCopyImageInfo2-apiVersion-07933

    If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
    `srcImage` and `dstImage` **must** have the same [VkImageType](resources.html#VkImageType)

* 
[](#VUID-VkCopyImageInfo2-apiVersion-08969) VUID-VkCopyImageInfo2-apiVersion-08969

    If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
    `srcImage` or `dstImage` is of type `VK_IMAGE_TYPE_2D`, then
    for each element of `pRegions`, `extent.depth` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-srcImage-07743) VUID-VkCopyImageInfo2-srcImage-07743

If `srcImage` and `dstImage` have a different [VkImageType](resources.html#VkImageType),
and the [`maintenance5`](features.html#features-maintenance5) feature is not
enabled,
one **must** be `VK_IMAGE_TYPE_3D` and the other **must** be
`VK_IMAGE_TYPE_2D`

* 
[](#VUID-VkCopyImageInfo2-srcImage-08793) VUID-VkCopyImageInfo2-srcImage-08793

If `srcImage` and `dstImage` have the same [VkImageType](resources.html#VkImageType),
for each element of `pRegions`,
if neither of the `layerCount` members of `srcSubresource` or
`dstSubresource` are `VK_REMAINING_ARRAY_LAYERS`,
the `layerCount` members of `srcSubresource` or
`dstSubresource` **must** match

* 
[](#VUID-VkCopyImageInfo2-srcImage-08794) VUID-VkCopyImageInfo2-srcImage-08794

If `srcImage` and `dstImage` have the same [VkImageType](resources.html#VkImageType),
and one of the `layerCount` members of `srcSubresource` or
`dstSubresource` is `VK_REMAINING_ARRAY_LAYERS`, the other
member **must** be either `VK_REMAINING_ARRAY_LAYERS` or equal to the
`arrayLayers` member of the [VkImageCreateInfo](resources.html#VkImageCreateInfo) used to create
the image minus `baseArrayLayer`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01790) VUID-VkCopyImageInfo2-srcImage-01790

If `srcImage` and `dstImage` are both of type
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`extent.depth` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01791) VUID-VkCopyImageInfo2-srcImage-01791

If `srcImage` is of type `VK_IMAGE_TYPE_2D`, and `dstImage`
is of type `VK_IMAGE_TYPE_3D`, then for each element of
`pRegions`, `extent.depth` **must** equal
`srcSubresource.layerCount`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01792) VUID-VkCopyImageInfo2-dstImage-01792

If `dstImage` is of type `VK_IMAGE_TYPE_2D`, and `srcImage`
is of type `VK_IMAGE_TYPE_3D`, then for each element of
`pRegions`, `extent.depth` **must** equal
`dstSubresource.layerCount`

* 
[](#VUID-VkCopyImageInfo2-dstOffset-00150) VUID-VkCopyImageInfo2-dstOffset-00150

For each element of `pRegions`, `dstOffset.x` and
(`extent.width` +  `dstOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-dstOffset-00151) VUID-VkCopyImageInfo2-dstOffset-00151

For each element of `pRegions`, `dstOffset.y` and
(`extent.height` +  `dstOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-dstImage-00152) VUID-VkCopyImageInfo2-dstImage-00152

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-VkCopyImageInfo2-dstOffset-00153) VUID-VkCopyImageInfo2-dstOffset-00153

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstOffset.z` and
(`extent.depth` +  `dstOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-pRegions-07278) VUID-VkCopyImageInfo2-pRegions-07278

For each element of `pRegions`, `srcOffset.x` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-pRegions-07279) VUID-VkCopyImageInfo2-pRegions-07279

For each element of `pRegions`, `srcOffset.y` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-pRegions-07280) VUID-VkCopyImageInfo2-pRegions-07280

For each element of `pRegions`, `srcOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-pRegions-07281) VUID-VkCopyImageInfo2-pRegions-07281

For each element of `pRegions`, `dstOffset.x` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-pRegions-07282) VUID-VkCopyImageInfo2-pRegions-07282

For each element of `pRegions`, `dstOffset.y` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-pRegions-07283) VUID-VkCopyImageInfo2-pRegions-07283

For each element of `pRegions`, `dstOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01728) VUID-VkCopyImageInfo2-srcImage-01728

For each element of `pRegions`, if the sum of `srcOffset.x` and
`extent.width` does not equal the width of the subresource specified
by `srcSubresource`, `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01729) VUID-VkCopyImageInfo2-srcImage-01729

For each element of `pRegions`, if the sum of `srcOffset.y` and
`extent.height` does not equal the height of the subresource
specified by `srcSubresource`, `extent.height` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-srcImage-01730) VUID-VkCopyImageInfo2-srcImage-01730

For each element of `pRegions`, if the sum of `srcOffset.z` and
`extent.depth` does not equal the depth of the subresource specified
by `srcSubresource`, `extent.depth` **must** be a multiple of the
[texel block extent depth](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01732) VUID-VkCopyImageInfo2-dstImage-01732

For each element of `pRegions`, if the sum of `dstOffset.x` and
`extent.width` does not equal the width of the subresource specified
by `dstSubresource`, `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01733) VUID-VkCopyImageInfo2-dstImage-01733

For each element of `pRegions`, if the sum of `dstOffset.y` and
`extent.height` does not equal the height of the subresource
specified by `dstSubresource`, `extent.height` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-dstImage-01734) VUID-VkCopyImageInfo2-dstImage-01734

For each element of `pRegions`, if the sum of `dstOffset.z` and
`extent.depth` does not equal the depth of the subresource specified
by `dstSubresource`, `extent.depth` **must** be a multiple of the
[texel block extent depth](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageInfo2-aspect-06662) VUID-VkCopyImageInfo2-aspect-06662

If the `aspect` member of any element of `pRegions` includes any
flag other than `VK_IMAGE_ASPECT_STENCIL_BIT` or `srcImage` was
not created with [separate stencil    usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` **must** have been included in the
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage` used to create `srcImage`

* 
[](#VUID-VkCopyImageInfo2-aspect-06663) VUID-VkCopyImageInfo2-aspect-06663

If the `aspect` member of any element of `pRegions` includes any
flag other than `VK_IMAGE_ASPECT_STENCIL_BIT` or `dstImage` was
not created with [separate stencil    usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` **must** have been included in the
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage` used to create `dstImage`

* 
[](#VUID-VkCopyImageInfo2-aspect-06664) VUID-VkCopyImageInfo2-aspect-06664

If the `aspect` member of any element of `pRegions` includes
`VK_IMAGE_ASPECT_STENCIL_BIT`, and `srcImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` **must** have been included in the
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage` used to create
`srcImage`

* 
[](#VUID-VkCopyImageInfo2-aspect-06665) VUID-VkCopyImageInfo2-aspect-06665

If the `aspect` member of any element of `pRegions` includes
`VK_IMAGE_ASPECT_STENCIL_BIT`, and `dstImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` **must** have been included in the
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage` used to create
`dstImage`

* 
[](#VUID-VkCopyImageInfo2-srcImage-07966) VUID-VkCopyImageInfo2-srcImage-07966

If `srcImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyImageInfo2-srcSubresource-07967) VUID-VkCopyImageInfo2-srcSubresource-07967

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageInfo2-srcSubresource-07968) VUID-VkCopyImageInfo2-srcSubresource-07968

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageInfo2-srcImage-07969) VUID-VkCopyImageInfo2-srcImage-07969

`srcImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkCopyImageInfo2-dstImage-07966) VUID-VkCopyImageInfo2-dstImage-07966

If `dstImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyImageInfo2-dstSubresource-07967) VUID-VkCopyImageInfo2-dstSubresource-07967

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyImageInfo2-dstSubresource-07968) VUID-VkCopyImageInfo2-dstSubresource-07968

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyImageInfo2-dstImage-07969) VUID-VkCopyImageInfo2-dstImage-07969

`dstImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

Valid Usage (Implicit)

* 
[](#VUID-VkCopyImageInfo2-sType-sType) VUID-VkCopyImageInfo2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_IMAGE_INFO_2`

* 
[](#VUID-VkCopyImageInfo2-pNext-pNext) VUID-VkCopyImageInfo2-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkCopyImageInfo2-srcImage-parameter) VUID-VkCopyImageInfo2-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyImageInfo2-srcImageLayout-parameter) VUID-VkCopyImageInfo2-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyImageInfo2-dstImage-parameter) VUID-VkCopyImageInfo2-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyImageInfo2-dstImageLayout-parameter) VUID-VkCopyImageInfo2-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyImageInfo2-pRegions-parameter) VUID-VkCopyImageInfo2-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageCopy2](#VkImageCopy2) structures

* 
[](#VUID-VkCopyImageInfo2-regionCount-arraylength) VUID-VkCopyImageInfo2-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkCopyImageInfo2-commonparent) VUID-VkCopyImageInfo2-commonparent

 Both of `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

The `VkImageCopy2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkImageCopy2 {
    VkStructureType             sType;
    const void*                 pNext;
    VkImageSubresourceLayers    srcSubresource;
    VkOffset3D                  srcOffset;
    VkImageSubresourceLayers    dstSubresource;
    VkOffset3D                  dstOffset;
    VkExtent3D                  extent;
} VkImageCopy2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkImageCopy2 VkImageCopy2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcSubresource` and `dstSubresource` are
[VkImageSubresourceLayers](#VkImageSubresourceLayers) structures specifying the image
subresources of the images used for the source and destination image
data, respectively.

* 
`srcOffset` and `dstOffset` select the initial `x`, `y`,
and `z` offsets in texels of the sub-regions of the source and
destination image data.

* 
`extent` is the size in texels of the image to copy in `width`,
`height` and `depth`.

Valid Usage

* 
[](#VUID-VkImageCopy2-apiVersion-07940) VUID-VkImageCopy2-apiVersion-07940

If
    the [VK_KHR_sampler_ycbcr_conversion](../appendices/extensions.html#VK_KHR_sampler_ycbcr_conversion) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
the
    `aspectMask` member of `srcSubresource` and `dstSubresource`
    **must** match

* 
[](#VUID-VkImageCopy2-apiVersion-07941) VUID-VkImageCopy2-apiVersion-07941

If
    the [VK_KHR_maintenance1](../appendices/extensions.html#VK_KHR_maintenance1) extension is not enabled,
and
    [VkPhysicalDeviceProperties](devsandqueues.html#VkPhysicalDeviceProperties)::`apiVersion` is less than Vulkan
    1.1,
the
    `layerCount` member of `srcSubresource` and `dstSubresource`
    **must** match

* 
[](#VUID-VkImageCopy2-extent-06668) VUID-VkImageCopy2-extent-06668

`extent.width` **must** not be 0

* 
[](#VUID-VkImageCopy2-extent-06669) VUID-VkImageCopy2-extent-06669

`extent.height` **must** not be 0

* 
[](#VUID-VkImageCopy2-extent-06670) VUID-VkImageCopy2-extent-06670

`extent.depth` **must** not be 0

Valid Usage (Implicit)

* 
[](#VUID-VkImageCopy2-sType-sType) VUID-VkImageCopy2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_IMAGE_COPY_2`

* 
[](#VUID-VkImageCopy2-pNext-pNext) VUID-VkImageCopy2-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkImageCopy2-srcSubresource-parameter) VUID-VkImageCopy2-srcSubresource-parameter

 `srcSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

* 
[](#VUID-VkImageCopy2-dstSubresource-parameter) VUID-VkImageCopy2-dstSubresource-parameter

 `dstSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

Data **can** be copied between buffers and images, enabling applications to
load and store data between images and application-defined offsets in buffer
memory.

When copying between a buffer and an image, texels in the image and bytes in
the buffer are accessed as follows.

Texels at each coordinate (x,y,z,layer) in the image subresource are
accessed, where:

x is in the range [`imageOffset.x`,
`imageOffset.x` +  `imageExtent.width`),

y is in the range [`imageOffset.y`,
`imageOffset.y` +  `imageExtent.height`),

z is in the range [`imageOffset.z`,
`imageOffset.z` +  `imageExtent.depth`),

layer is in the range
[`imageSubresource.baseArrayLayer`,
`imageSubresource.baseArrayLayer` + 
`imageSubresource.layerCount`)

For each (x,y,z,layer) coordinate in the image, bytes in the buffer
are accessed at offsets in the range [texelOffset, texelOffset + 
blockSize), where:

texelOffset = `bufferOffset` +  (⌊(x -
imageOffset.x) / blockWidth⌋ × blockSize) + 
(⌊(y - imageOffset.y) / blockHeight⌋ ×
rowExtent) +  (⌊(z - imageOffset.z) /
blockDepth⌋ × sliceExtent) +  ((layer -
`imageSubresource.baseArrayLayer`) × layerExtent)

rowExtent = ⌈ max(`bufferRowLength`,
`imageExtent.width`) / blockWidth ⌉ × blockSize

sliceExtent = ⌈ max(`bufferImageHeight`,
`imageExtent.height`) / blockHeight ⌉ ×
rowExtent

layerExtent = ⌈ `imageExtent.depth` / blockDepth
⌉ × sliceExtent

and where blockSize, blockWidth, blockHeight, and
blockDepth are the [texel block size and extents](formats.html#formats-compatibility-classes) of the image’s format.

Image Rotation Addressing
If a rotation is specified by [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM), the 2D
region of the image being addressed is rotated around the offset, and texels
at each coordinate (x',y',z',layer) are accessed in the image
subresource instead, where:

* 
If `VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` is specified, no rotation
is performed:

x' is in the same range as x

y' is in the same range as y

* 
If `VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR` is specified

x' is in the range [`imageOffset.x` - 
`imageExtent.height`, `imageOffset.x`)

y' is in the range [`imageOffset.y`,
`imageOffset.y` +  `imageExtent.width`)

* 
If `VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` is specified:

x' is in the range [`imageOffset.x` - 
`imageExtent.width`, `imageOffset.x`)

y' is in the range [`imageOffset.y` - 
`imageExtent.height`, `imageOffset.y`)

* 
If `VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` is specified:

x' is in the range [`imageOffset.x`,
`imageOffset.x` +  `imageExtent.height`)

y' is in the range [`imageOffset.y` - 
`imageExtent.width`, `imageOffset.y`)

Buffer addressing calculations are unaffected by this rotation.

When copying between a buffer and the depth or stencil aspect of an image,
data in the buffer is assumed to be laid out as separate planes rather than
interleaved.
Addressing calculations are thus performed for a different format than the
base image, according to the aspect, as described in the following table:

Table 1. Depth/Stencil Aspect Copy Table

Base Format
Depth Aspect Format
Stencil Aspect Format

`VK_FORMAT_D16_UNORM`
`VK_FORMAT_D16_UNORM`
-

`VK_FORMAT_X8_D24_UNORM_PACK32`
`VK_FORMAT_X8_D24_UNORM_PACK32`
-

`VK_FORMAT_D32_SFLOAT`
`VK_FORMAT_D32_SFLOAT`
-

`VK_FORMAT_S8_UINT`
-
`VK_FORMAT_S8_UINT`

`VK_FORMAT_D16_UNORM_S8_UINT`
`VK_FORMAT_D16_UNORM`
`VK_FORMAT_S8_UINT`

`VK_FORMAT_D24_UNORM_S8_UINT`
`VK_FORMAT_X8_D24_UNORM_PACK32`
`VK_FORMAT_S8_UINT`

`VK_FORMAT_D32_SFLOAT_S8_UINT`
`VK_FORMAT_D32_SFLOAT`
`VK_FORMAT_S8_UINT`

When copying between a buffer and any plane of a [multi-planar image](formats.html#formats-multiplanar), addressing calculations are performed using the
[compatible format for that plane](formats.html#formats-compatible-planes), rather than
the format of the multi-planar image.

Each texel block is copied from one resource to the other according to the
above addressing equations.

To copy data from a buffer object to an image object, call:

// Provided by VK_VERSION_1_0
void vkCmdCopyBufferToImage(
    VkCommandBuffer                             commandBuffer,
    VkBuffer                                    srcBuffer,
    VkImage                                     dstImage,
    VkImageLayout                               dstImageLayout,
    uint32_t                                    regionCount,
    const VkBufferImageCopy*                    pRegions);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`srcBuffer` is the source buffer.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the copy.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkBufferImageCopy](#VkBufferImageCopy)
structures specifying the regions to copy.

Each source region specified by `pRegions` is copied from the source
buffer to the destination region of the destination image according to the
[addressing calculations](#copies-buffers-images-addressing) for each
resource.
If any of the specified regions in `srcBuffer` overlaps in memory with
any of the specified regions in `dstImage`, values read from those
overlapping regions are **undefined**.
If any region accesses a depth aspect in `dstImage`
and the `[VK_EXT_depth_range_unrestricted](../appendices/extensions.html#VK_EXT_depth_range_unrestricted)` extension is not enabled,
values copied from `srcBuffer` outside of the range [0,1] will be
written as **undefined** values to the destination image.

Copy regions for the image **must** be aligned to a multiple of the texel block
extent in each dimension, except at the edges of the image, where region
extents **must** match the edge of the image.

Valid Usage

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07966) VUID-vkCmdCopyBufferToImage-dstImage-07966

If `dstImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyBufferToImage-imageSubresource-07967) VUID-vkCmdCopyBufferToImage-imageSubresource-07967

The `imageSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdCopyBufferToImage-imageSubresource-07968) VUID-vkCmdCopyBufferToImage-imageSubresource-07968

If `imageSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`imageSubresource.baseArrayLayer` + 
`imageSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07969) VUID-vkCmdCopyBufferToImage-dstImage-07969

`dstImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-vkCmdCopyBufferToImage-imageSubresource-07970) VUID-vkCmdCopyBufferToImage-imageSubresource-07970

The image region specified by each element of `pRegions` **must** be
contained within the specified `imageSubresource` of
`dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageSubresource-07971) VUID-vkCmdCopyBufferToImage-imageSubresource-07971

For each element of `pRegions`, `imageOffset.x` and
(`imageExtent.width` +  `imageOffset.x`) **must**
both be greater than or equal to `0` and less than or equal to the width
of the specified `imageSubresource` of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageSubresource-07972) VUID-vkCmdCopyBufferToImage-imageSubresource-07972

For each element of `pRegions`, `imageOffset.y` and
(`imageExtent.height` +  `imageOffset.y`) **must**
both be greater than or equal to `0` and less than or equal to the
height of the specified `imageSubresource` of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07973) VUID-vkCmdCopyBufferToImage-dstImage-07973

`dstImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-01828) VUID-vkCmdCopyBufferToImage-commandBuffer-01828

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-01829) VUID-vkCmdCopyBufferToImage-commandBuffer-01829

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-01830) VUID-vkCmdCopyBufferToImage-commandBuffer-01830

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-07737) VUID-vkCmdCopyBufferToImage-commandBuffer-07737

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT` or `VK_QUEUE_COMPUTE_BIT`, the
`bufferOffset` member of any element of `pRegions` **must** be a
multiple of `4`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-07738) VUID-vkCmdCopyBufferToImage-imageOffset-07738

The `imageOffset` and `imageExtent` members of each element of
`pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-07739) VUID-vkCmdCopyBufferToImage-commandBuffer-07739

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pRegions`, the
`aspectMask` member of `imageSubresource` **must** not be
`VK_IMAGE_ASPECT_DEPTH_BIT` or `VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyBufferToImage-pRegions-00171) VUID-vkCmdCopyBufferToImage-pRegions-00171

`srcBuffer` **must** be large enough to contain all buffer locations
that are accessed according to [Buffer    and Image Addressing](#copies-buffers-images-addressing), for each element of `pRegions`

* 
[](#VUID-vkCmdCopyBufferToImage-pRegions-00173) VUID-vkCmdCopyBufferToImage-pRegions-00173

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-vkCmdCopyBufferToImage-srcBuffer-00174) VUID-vkCmdCopyBufferToImage-srcBuffer-00174

`srcBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-01997) VUID-vkCmdCopyBufferToImage-dstImage-01997

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_DST_BIT`

* 
[](#VUID-vkCmdCopyBufferToImage-srcBuffer-00176) VUID-vkCmdCopyBufferToImage-srcBuffer-00176

If `srcBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-00177) VUID-vkCmdCopyBufferToImage-dstImage-00177

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdCopyBufferToImage-dstImageLayout-00180) VUID-vkCmdCopyBufferToImage-dstImageLayout-00180

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImageLayout-01396) VUID-vkCmdCopyBufferToImage-dstImageLayout-01396

`dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdCopyBufferToImage-pRegions-07931) VUID-vkCmdCopyBufferToImage-pRegions-07931

If [VK_EXT_depth_range_unrestricted](../appendices/extensions.html#VK_EXT_depth_range_unrestricted) is not enabled, for
each element of `pRegions` whose `imageSubresource` contains a
depth aspect, the data in `srcBuffer` **must** be in the range
[0,1]

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07979) VUID-vkCmdCopyBufferToImage-dstImage-07979

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `imageOffset.y` **must** be `0` and
`imageExtent.height` **must** be `1`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-09104) VUID-vkCmdCopyBufferToImage-imageOffset-09104

For each element of `pRegions`, `imageOffset.z` and
(`imageExtent.depth` +  `imageOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `imageSubresource` of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07980) VUID-vkCmdCopyBufferToImage-dstImage-07980

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`imageOffset.z` **must** be `0` and `imageExtent.depth` **must**
be `1`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07274) VUID-vkCmdCopyBufferToImage-dstImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`imageOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10051) VUID-vkCmdCopyBufferToImage-imageOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `imageOffset.x`
does not equal the width of the subresource specified by
`imageSubresource`, `imageOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07275) VUID-vkCmdCopyBufferToImage-dstImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`imageOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10052) VUID-vkCmdCopyBufferToImage-imageOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `imageOffset.y`
does not equal the height of the subresource specified by
`imageSubresource`, `imageOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07276) VUID-vkCmdCopyBufferToImage-dstImage-07276

For each element of `pRegions`, `imageOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-00207) VUID-vkCmdCopyBufferToImage-dstImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `imageOffset.x` and `extent.width` does not equal
the width of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10053) VUID-vkCmdCopyBufferToImage-imageOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`imageOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10054) VUID-vkCmdCopyBufferToImage-imageOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10055) VUID-vkCmdCopyBufferToImage-imageOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`imageOffset.x` and `extent.height` does not equal the width
of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-00208) VUID-vkCmdCopyBufferToImage-dstImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `imageOffset.y` and `extent.height` does not equal
the height of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10056) VUID-vkCmdCopyBufferToImage-imageOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`imageOffset.y` and `extent.width` does not equal the height
of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10057) VUID-vkCmdCopyBufferToImage-imageOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageOffset-10058) VUID-vkCmdCopyBufferToImage-imageOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`imageOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-00209) VUID-vkCmdCopyBufferToImage-dstImage-00209

For each element of `pRegions`, if the sum of `imageOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-imageSubresource-09105) VUID-vkCmdCopyBufferToImage-imageSubresource-09105

For each element of `pRegions`, `imageSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07981) VUID-vkCmdCopyBufferToImage-dstImage-07981

If `dstImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`imageSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07983) VUID-vkCmdCopyBufferToImage-dstImage-07983

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `imageSubresource.baseArrayLayer` **must**
be `0` and `imageSubresource.layerCount` **must** be `1`

* 
[](#VUID-vkCmdCopyBufferToImage-bufferRowLength-09106) VUID-vkCmdCopyBufferToImage-bufferRowLength-09106

For each element of `pRegions`, `bufferRowLength` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-bufferImageHeight-09107) VUID-vkCmdCopyBufferToImage-bufferImageHeight-09107

For each element of `pRegions`, `bufferImageHeight` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-vkCmdCopyBufferToImage-bufferRowLength-09108) VUID-vkCmdCopyBufferToImage-bufferRowLength-09108

For each element of `pRegions`, `bufferRowLength` divided by
the [texel block extent width](formats.html#formats-compatibility-classes) and then
multiplied by the texel block size of `dstImage` **must** be less
than or equal to 231-1

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07975) VUID-vkCmdCopyBufferToImage-dstImage-07975

If `dstImage` does not have either a depth/stencil format
or a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `bufferOffset` **must** be a
multiple of the [texel block size](formats.html#formats-compatibility-classes)

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07976) VUID-vkCmdCopyBufferToImage-dstImage-07976

If `dstImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`, `bufferOffset`
**must** be a multiple of the element size of the compatible format for the
format and the `aspectMask` of the `imageSubresource` as defined
in [Compatible Formats of Planes of Multi-Planar Formats](formats.html#formats-compatible-planes)

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-07978) VUID-vkCmdCopyBufferToImage-dstImage-07978

If `dstImage` has a depth/stencil format, the `bufferOffset`
member of any element of `pRegions` **must** be a multiple of `4`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-parameter) VUID-vkCmdCopyBufferToImage-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyBufferToImage-srcBuffer-parameter) VUID-vkCmdCopyBufferToImage-srcBuffer-parameter

 `srcBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-vkCmdCopyBufferToImage-dstImage-parameter) VUID-vkCmdCopyBufferToImage-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdCopyBufferToImage-dstImageLayout-parameter) VUID-vkCmdCopyBufferToImage-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdCopyBufferToImage-pRegions-parameter) VUID-vkCmdCopyBufferToImage-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkBufferImageCopy](#VkBufferImageCopy) structures

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-recording) VUID-vkCmdCopyBufferToImage-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyBufferToImage-commandBuffer-cmdpool) VUID-vkCmdCopyBufferToImage-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyBufferToImage-renderpass) VUID-vkCmdCopyBufferToImage-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyBufferToImage-videocoding) VUID-vkCmdCopyBufferToImage-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdCopyBufferToImage-regionCount-arraylength) VUID-vkCmdCopyBufferToImage-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-vkCmdCopyBufferToImage-commonparent) VUID-vkCmdCopyBufferToImage-commonparent

 Each of `commandBuffer`, `dstImage`, and `srcBuffer` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

To copy data from an image object to a buffer object, call:

// Provided by VK_VERSION_1_0
void vkCmdCopyImageToBuffer(
    VkCommandBuffer                             commandBuffer,
    VkImage                                     srcImage,
    VkImageLayout                               srcImageLayout,
    VkBuffer                                    dstBuffer,
    uint32_t                                    regionCount,
    const VkBufferImageCopy*                    pRegions);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the copy.

* 
`dstBuffer` is the destination buffer.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkBufferImageCopy](#VkBufferImageCopy)
structures specifying the regions to copy.

Each source region specified by `pRegions` is copied from the source
image to the destination region of the destination buffer according to the
[addressing calculations](#copies-buffers-images-addressing) for each
resource.
If any of the specified regions in `srcImage` overlaps in memory with
any of the specified regions in `dstBuffer`, values read from those
overlapping regions are **undefined**.

Copy regions for the image **must** be aligned to a multiple of the texel block
extent in each dimension, except at the edges of the image, where region
extents **must** match the edge of the image.

Valid Usage

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07966) VUID-vkCmdCopyImageToBuffer-srcImage-07966

If `srcImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyImageToBuffer-imageSubresource-07967) VUID-vkCmdCopyImageToBuffer-imageSubresource-07967

The `imageSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdCopyImageToBuffer-imageSubresource-07968) VUID-vkCmdCopyImageToBuffer-imageSubresource-07968

If `imageSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`imageSubresource.baseArrayLayer` + 
`imageSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07969) VUID-vkCmdCopyImageToBuffer-srcImage-07969

`srcImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageSubresource-07970) VUID-vkCmdCopyImageToBuffer-imageSubresource-07970

The image region specified by each element of `pRegions` **must** be
contained within the specified `imageSubresource` of
`srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageSubresource-07971) VUID-vkCmdCopyImageToBuffer-imageSubresource-07971

For each element of `pRegions`, `imageOffset.x` and
(`imageExtent.width` +  `imageOffset.x`) **must**
both be greater than or equal to `0` and less than or equal to the width
of the specified `imageSubresource` of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageSubresource-07972) VUID-vkCmdCopyImageToBuffer-imageSubresource-07972

For each element of `pRegions`, `imageOffset.y` and
(`imageExtent.height` +  `imageOffset.y`) **must**
both be greater than or equal to `0` and less than or equal to the
height of the specified `imageSubresource` of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07973) VUID-vkCmdCopyImageToBuffer-srcImage-07973

`srcImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-01831) VUID-vkCmdCopyImageToBuffer-commandBuffer-01831

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-01832) VUID-vkCmdCopyImageToBuffer-commandBuffer-01832

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-01833) VUID-vkCmdCopyImageToBuffer-commandBuffer-01833

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be an unprotected buffer

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-07746) VUID-vkCmdCopyImageToBuffer-commandBuffer-07746

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT` or `VK_QUEUE_COMPUTE_BIT`, the
`bufferOffset` member of any element of `pRegions` **must** be a
multiple of `4`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-07747) VUID-vkCmdCopyImageToBuffer-imageOffset-07747

The `imageOffset` and `imageExtent` members of each element of
`pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-10216) VUID-vkCmdCopyImageToBuffer-commandBuffer-10216

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pRegions`, the
`aspectMask` member of `imageSubresource` **must** not be
`VK_IMAGE_ASPECT_DEPTH_BIT` or `VK_IMAGE_ASPECT_STENCIL_BIT`

* 
[](#VUID-vkCmdCopyImageToBuffer-pRegions-00183) VUID-vkCmdCopyImageToBuffer-pRegions-00183

`dstBuffer` **must** be large enough to contain all buffer locations
that are accessed according to [Buffer    and Image Addressing](#copies-buffers-images-addressing), for each element of `pRegions`

* 
[](#VUID-vkCmdCopyImageToBuffer-pRegions-00184) VUID-vkCmdCopyImageToBuffer-pRegions-00184

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-00186) VUID-vkCmdCopyImageToBuffer-srcImage-00186

`srcImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-01998) VUID-vkCmdCopyImageToBuffer-srcImage-01998

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_SRC_BIT`

* 
[](#VUID-vkCmdCopyImageToBuffer-dstBuffer-00191) VUID-vkCmdCopyImageToBuffer-dstBuffer-00191

`dstBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdCopyImageToBuffer-dstBuffer-00192) VUID-vkCmdCopyImageToBuffer-dstBuffer-00192

If `dstBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImageLayout-00189) VUID-vkCmdCopyImageToBuffer-srcImageLayout-00189

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImageLayout-01397) VUID-vkCmdCopyImageToBuffer-srcImageLayout-01397

`srcImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07979) VUID-vkCmdCopyImageToBuffer-srcImage-07979

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `imageOffset.y` **must** be `0` and
`imageExtent.height` **must** be `1`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-09104) VUID-vkCmdCopyImageToBuffer-imageOffset-09104

For each element of `pRegions`, `imageOffset.z` and
(`imageExtent.depth` +  `imageOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `imageSubresource` of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07980) VUID-vkCmdCopyImageToBuffer-srcImage-07980

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`imageOffset.z` **must** be `0` and `imageExtent.depth` **must**
be `1`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07274) VUID-vkCmdCopyImageToBuffer-srcImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`imageOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10051) VUID-vkCmdCopyImageToBuffer-imageOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `imageOffset.x`
does not equal the width of the subresource specified by
`imageSubresource`, `imageOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07275) VUID-vkCmdCopyImageToBuffer-srcImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`imageOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10052) VUID-vkCmdCopyImageToBuffer-imageOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `imageOffset.y`
does not equal the height of the subresource specified by
`imageSubresource`, `imageOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07276) VUID-vkCmdCopyImageToBuffer-srcImage-07276

For each element of `pRegions`, `imageOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-00207) VUID-vkCmdCopyImageToBuffer-srcImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `imageOffset.x` and `extent.width` does not equal
the width of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10053) VUID-vkCmdCopyImageToBuffer-imageOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`imageOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10054) VUID-vkCmdCopyImageToBuffer-imageOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10055) VUID-vkCmdCopyImageToBuffer-imageOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`imageOffset.x` and `extent.height` does not equal the width
of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-00208) VUID-vkCmdCopyImageToBuffer-srcImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `imageOffset.y` and `extent.height` does not equal
the height of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10056) VUID-vkCmdCopyImageToBuffer-imageOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`imageOffset.y` and `extent.width` does not equal the height
of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10057) VUID-vkCmdCopyImageToBuffer-imageOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageOffset-10058) VUID-vkCmdCopyImageToBuffer-imageOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`imageOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-00209) VUID-vkCmdCopyImageToBuffer-srcImage-00209

For each element of `pRegions`, if the sum of `imageOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-imageSubresource-09105) VUID-vkCmdCopyImageToBuffer-imageSubresource-09105

For each element of `pRegions`, `imageSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07981) VUID-vkCmdCopyImageToBuffer-srcImage-07981

If `srcImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`imageSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07983) VUID-vkCmdCopyImageToBuffer-srcImage-07983

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `imageSubresource.baseArrayLayer` **must**
be `0` and `imageSubresource.layerCount` **must** be `1`

* 
[](#VUID-vkCmdCopyImageToBuffer-bufferRowLength-09106) VUID-vkCmdCopyImageToBuffer-bufferRowLength-09106

For each element of `pRegions`, `bufferRowLength` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-bufferImageHeight-09107) VUID-vkCmdCopyImageToBuffer-bufferImageHeight-09107

For each element of `pRegions`, `bufferImageHeight` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-vkCmdCopyImageToBuffer-bufferRowLength-09108) VUID-vkCmdCopyImageToBuffer-bufferRowLength-09108

For each element of `pRegions`, `bufferRowLength` divided by
the [texel block extent width](formats.html#formats-compatibility-classes) and then
multiplied by the texel block size of `srcImage` **must** be less
than or equal to 231-1

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07975) VUID-vkCmdCopyImageToBuffer-srcImage-07975

If `srcImage` does not have either a depth/stencil format
or a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `bufferOffset` **must** be a
multiple of the [texel block size](formats.html#formats-compatibility-classes)

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07976) VUID-vkCmdCopyImageToBuffer-srcImage-07976

If `srcImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`, `bufferOffset`
**must** be a multiple of the element size of the compatible format for the
format and the `aspectMask` of the `imageSubresource` as defined
in [Compatible Formats of Planes of Multi-Planar Formats](formats.html#formats-compatible-planes)

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-07978) VUID-vkCmdCopyImageToBuffer-srcImage-07978

If `srcImage` has a depth/stencil format, the `bufferOffset`
member of any element of `pRegions` **must** be a multiple of `4`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-parameter) VUID-vkCmdCopyImageToBuffer-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImage-parameter) VUID-vkCmdCopyImageToBuffer-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdCopyImageToBuffer-srcImageLayout-parameter) VUID-vkCmdCopyImageToBuffer-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdCopyImageToBuffer-dstBuffer-parameter) VUID-vkCmdCopyImageToBuffer-dstBuffer-parameter

 `dstBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-vkCmdCopyImageToBuffer-pRegions-parameter) VUID-vkCmdCopyImageToBuffer-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkBufferImageCopy](#VkBufferImageCopy) structures

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-recording) VUID-vkCmdCopyImageToBuffer-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyImageToBuffer-commandBuffer-cmdpool) VUID-vkCmdCopyImageToBuffer-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyImageToBuffer-renderpass) VUID-vkCmdCopyImageToBuffer-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyImageToBuffer-videocoding) VUID-vkCmdCopyImageToBuffer-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdCopyImageToBuffer-regionCount-arraylength) VUID-vkCmdCopyImageToBuffer-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-vkCmdCopyImageToBuffer-commonparent) VUID-vkCmdCopyImageToBuffer-commonparent

 Each of `commandBuffer`, `dstBuffer`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

For both [vkCmdCopyBufferToImage](#vkCmdCopyBufferToImage) and [vkCmdCopyImageToBuffer](#vkCmdCopyImageToBuffer), each
element of `pRegions` is a structure defined as:

// Provided by VK_VERSION_1_0
typedef struct VkBufferImageCopy {
    VkDeviceSize                bufferOffset;
    uint32_t                    bufferRowLength;
    uint32_t                    bufferImageHeight;
    VkImageSubresourceLayers    imageSubresource;
    VkOffset3D                  imageOffset;
    VkExtent3D                  imageExtent;
} VkBufferImageCopy;

* 
`bufferOffset` is the offset in bytes from the start of the buffer
object where the image data is copied from or to.

* 
`bufferRowLength` and `bufferImageHeight` specify in texels a
subregion of a larger two- or three-dimensional image in buffer memory,
and control the addressing calculations.
If either of these values is zero, that aspect of the buffer memory is
considered to be tightly packed according to the `imageExtent`.

* 
`imageSubresource` is a [VkImageSubresourceLayers](#VkImageSubresourceLayers) used to
specify the specific image subresources of the image used for the source
or destination image data.

* 
`imageOffset` selects the initial `x`, `y`, `z` offsets
in texels of the sub-region of the source or destination image data.

* 
`imageExtent` is the size in texels of the image to copy in
`width`, `height` and `depth`.

Valid Usage

* 
[](#VUID-VkBufferImageCopy-bufferRowLength-09101) VUID-VkBufferImageCopy-bufferRowLength-09101

`bufferRowLength` **must** be `0`, or greater than or equal to the
`width` member of `imageExtent`

* 
[](#VUID-VkBufferImageCopy-bufferImageHeight-09102) VUID-VkBufferImageCopy-bufferImageHeight-09102

`bufferImageHeight` **must** be `0`, or greater than or equal to the
`height` member of `imageExtent`

* 
[](#VUID-VkBufferImageCopy-aspectMask-09103) VUID-VkBufferImageCopy-aspectMask-09103

The `aspectMask` member of `imageSubresource` **must** only have a
single bit set

* 
[](#VUID-VkBufferImageCopy-imageExtent-06659) VUID-VkBufferImageCopy-imageExtent-06659

`imageExtent.width` **must** not be 0

* 
[](#VUID-VkBufferImageCopy-imageExtent-06660) VUID-VkBufferImageCopy-imageExtent-06660

`imageExtent.height` **must** not be 0

* 
[](#VUID-VkBufferImageCopy-imageExtent-06661) VUID-VkBufferImageCopy-imageExtent-06661

`imageExtent.depth` **must** not be 0

Valid Usage (Implicit)

* 
[](#VUID-VkBufferImageCopy-imageSubresource-parameter) VUID-VkBufferImageCopy-imageSubresource-parameter

 `imageSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

More extensible versions of the commands to copy between buffers and images
are defined below.

To copy data from a buffer object to an image object, call:

// Provided by VK_VERSION_1_3
void vkCmdCopyBufferToImage2(
    VkCommandBuffer                             commandBuffer,
    const VkCopyBufferToImageInfo2*             pCopyBufferToImageInfo);

or the equivalent command

// Provided by VK_KHR_copy_commands2
void vkCmdCopyBufferToImage2KHR(
    VkCommandBuffer                             commandBuffer,
    const VkCopyBufferToImageInfo2*             pCopyBufferToImageInfo);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`pCopyBufferToImageInfo` is a pointer to a
[VkCopyBufferToImageInfo2](#VkCopyBufferToImageInfo2) structure describing the copy parameters.

This command is functionally identical to [vkCmdCopyBufferToImage](#vkCmdCopyBufferToImage), but
includes extensible sub-structures that include `sType` and `pNext`
parameters, allowing them to be more easily extended.

Valid Usage

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-01828) VUID-vkCmdCopyBufferToImage2-commandBuffer-01828

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-01829) VUID-vkCmdCopyBufferToImage2-commandBuffer-01829

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-01830) VUID-vkCmdCopyBufferToImage2-commandBuffer-01830

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-07737) VUID-vkCmdCopyBufferToImage2-commandBuffer-07737

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT` or `VK_QUEUE_COMPUTE_BIT`, the
`bufferOffset` member of any element of `pCopyBufferToImageInfo->pRegions` **must** be a
multiple of `4`

* 
[](#VUID-vkCmdCopyBufferToImage2-imageOffset-07738) VUID-vkCmdCopyBufferToImage2-imageOffset-07738

The `imageOffset` and `imageExtent` members of each element of
`pCopyBufferToImageInfo->pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-07739) VUID-vkCmdCopyBufferToImage2-commandBuffer-07739

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pCopyBufferToImageInfo->pRegions`, the
`aspectMask` member of `imageSubresource` **must** not be
`VK_IMAGE_ASPECT_DEPTH_BIT` or `VK_IMAGE_ASPECT_STENCIL_BIT`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-parameter) VUID-vkCmdCopyBufferToImage2-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyBufferToImage2-pCopyBufferToImageInfo-parameter) VUID-vkCmdCopyBufferToImage2-pCopyBufferToImageInfo-parameter

 `pCopyBufferToImageInfo` **must** be a valid pointer to a valid [VkCopyBufferToImageInfo2](#VkCopyBufferToImageInfo2) structure

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-recording) VUID-vkCmdCopyBufferToImage2-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyBufferToImage2-commandBuffer-cmdpool) VUID-vkCmdCopyBufferToImage2-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyBufferToImage2-renderpass) VUID-vkCmdCopyBufferToImage2-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyBufferToImage2-videocoding) VUID-vkCmdCopyBufferToImage2-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The `VkCopyBufferToImageInfo2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkCopyBufferToImageInfo2 {
    VkStructureType              sType;
    const void*                  pNext;
    VkBuffer                     srcBuffer;
    VkImage                      dstImage;
    VkImageLayout                dstImageLayout;
    uint32_t                     regionCount;
    const VkBufferImageCopy2*    pRegions;
} VkCopyBufferToImageInfo2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkCopyBufferToImageInfo2 VkCopyBufferToImageInfo2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcBuffer` is the source buffer.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the copy.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkBufferImageCopy2](#VkBufferImageCopy2)
structures specifying the regions to copy.

Valid Usage

* 
[](#VUID-VkCopyBufferToImageInfo2-pRegions-04565) VUID-VkCopyBufferToImageInfo2-pRegions-04565

The image region specified by each element of `pRegions`
that does not contain [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its
`pNext` chain
**must** be contained within the specified `imageSubresource` of
`dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2KHR-pRegions-04554) VUID-VkCopyBufferToImageInfo2KHR-pRegions-04554

If the image region specified by each element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, the
[rotated destination    region](#copies-buffers-images-rotation-addressing) **must** be contained within `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2KHR-pRegions-04555) VUID-VkCopyBufferToImageInfo2KHR-pRegions-04555

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`dstImage` **must** have a 1x1x1 [texel    block extent](formats.html#formats-compatibility-classes)

* 
[](#VUID-VkCopyBufferToImageInfo2KHR-pRegions-06203) VUID-VkCopyBufferToImageInfo2KHR-pRegions-06203

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`dstImage` **must** be of type `VK_IMAGE_TYPE_2D`

* 
[](#VUID-VkCopyBufferToImageInfo2KHR-pRegions-06204) VUID-VkCopyBufferToImageInfo2KHR-pRegions-06204

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`dstImage` **must** not have a [multi-planar    format](formats.html#formats-multiplanar)

* 
[](#VUID-VkCopyBufferToImageInfo2-pRegions-00171) VUID-VkCopyBufferToImageInfo2-pRegions-00171

`srcBuffer` **must** be large enough to contain all buffer locations
that are accessed according to [Buffer    and Image Addressing](#copies-buffers-images-addressing), for each element of `pRegions`

* 
[](#VUID-VkCopyBufferToImageInfo2-pRegions-00173) VUID-VkCopyBufferToImageInfo2-pRegions-00173

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-VkCopyBufferToImageInfo2-srcBuffer-00174) VUID-VkCopyBufferToImageInfo2-srcBuffer-00174

`srcBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-01997) VUID-VkCopyBufferToImageInfo2-dstImage-01997

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_DST_BIT`

* 
[](#VUID-VkCopyBufferToImageInfo2-srcBuffer-00176) VUID-VkCopyBufferToImageInfo2-srcBuffer-00176

If `srcBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-00177) VUID-VkCopyBufferToImageInfo2-dstImage-00177

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImageLayout-00180) VUID-VkCopyBufferToImageInfo2-dstImageLayout-00180

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImageLayout-01396) VUID-VkCopyBufferToImageInfo2-dstImageLayout-01396

`dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkCopyBufferToImageInfo2-pRegions-07931) VUID-VkCopyBufferToImageInfo2-pRegions-07931

If [VK_EXT_depth_range_unrestricted](../appendices/extensions.html#VK_EXT_depth_range_unrestricted) is not enabled, for
each element of `pRegions` whose `imageSubresource` contains a
depth aspect, the data in `srcBuffer` **must** be in the range
[0,1]

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07966) VUID-VkCopyBufferToImageInfo2-dstImage-07966

If `dstImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyBufferToImageInfo2-imageSubresource-07967) VUID-VkCopyBufferToImageInfo2-imageSubresource-07967

The `imageSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyBufferToImageInfo2-imageSubresource-07968) VUID-VkCopyBufferToImageInfo2-imageSubresource-07968

If `imageSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`imageSubresource.baseArrayLayer` + 
`imageSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07969) VUID-VkCopyBufferToImageInfo2-dstImage-07969

`dstImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07973) VUID-VkCopyBufferToImageInfo2-dstImage-07973

`dstImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07979) VUID-VkCopyBufferToImageInfo2-dstImage-07979

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `imageOffset.y` **must** be `0` and
`imageExtent.height` **must** be `1`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-09104) VUID-VkCopyBufferToImageInfo2-imageOffset-09104

For each element of `pRegions`, `imageOffset.z` and
(`imageExtent.depth` +  `imageOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `imageSubresource` of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07980) VUID-VkCopyBufferToImageInfo2-dstImage-07980

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`imageOffset.z` **must** be `0` and `imageExtent.depth` **must**
be `1`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07274) VUID-VkCopyBufferToImageInfo2-dstImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`imageOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10051) VUID-VkCopyBufferToImageInfo2-imageOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `imageOffset.x`
does not equal the width of the subresource specified by
`imageSubresource`, `imageOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07275) VUID-VkCopyBufferToImageInfo2-dstImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`imageOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10052) VUID-VkCopyBufferToImageInfo2-imageOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `imageOffset.y`
does not equal the height of the subresource specified by
`imageSubresource`, `imageOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07276) VUID-VkCopyBufferToImageInfo2-dstImage-07276

For each element of `pRegions`, `imageOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-00207) VUID-VkCopyBufferToImageInfo2-dstImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `imageOffset.x` and `extent.width` does not equal
the width of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10053) VUID-VkCopyBufferToImageInfo2-imageOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`imageOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10054) VUID-VkCopyBufferToImageInfo2-imageOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10055) VUID-VkCopyBufferToImageInfo2-imageOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`imageOffset.x` and `extent.height` does not equal the width
of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-00208) VUID-VkCopyBufferToImageInfo2-dstImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `imageOffset.y` and `extent.height` does not equal
the height of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10056) VUID-VkCopyBufferToImageInfo2-imageOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`imageOffset.y` and `extent.width` does not equal the height
of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10057) VUID-VkCopyBufferToImageInfo2-imageOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageOffset-10058) VUID-VkCopyBufferToImageInfo2-imageOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`imageOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-00209) VUID-VkCopyBufferToImageInfo2-dstImage-00209

For each element of `pRegions`, if the sum of `imageOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-imageSubresource-09105) VUID-VkCopyBufferToImageInfo2-imageSubresource-09105

For each element of `pRegions`, `imageSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07981) VUID-VkCopyBufferToImageInfo2-dstImage-07981

If `dstImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`imageSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07983) VUID-VkCopyBufferToImageInfo2-dstImage-07983

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `imageSubresource.baseArrayLayer` **must**
be `0` and `imageSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyBufferToImageInfo2-bufferRowLength-09106) VUID-VkCopyBufferToImageInfo2-bufferRowLength-09106

For each element of `pRegions`, `bufferRowLength` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-bufferImageHeight-09107) VUID-VkCopyBufferToImageInfo2-bufferImageHeight-09107

For each element of `pRegions`, `bufferImageHeight` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-bufferRowLength-09108) VUID-VkCopyBufferToImageInfo2-bufferRowLength-09108

For each element of `pRegions`, `bufferRowLength` divided by
the [texel block extent width](formats.html#formats-compatibility-classes) and then
multiplied by the texel block size of `dstImage` **must** be less
than or equal to 231-1

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07975) VUID-VkCopyBufferToImageInfo2-dstImage-07975

If `dstImage` does not have either a depth/stencil format
or a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `bufferOffset` **must** be a
multiple of the [texel block size](formats.html#formats-compatibility-classes)

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07976) VUID-VkCopyBufferToImageInfo2-dstImage-07976

If `dstImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`, `bufferOffset`
**must** be a multiple of the element size of the compatible format for the
format and the `aspectMask` of the `imageSubresource` as defined
in [Compatible Formats of Planes of Multi-Planar Formats](formats.html#formats-compatible-planes)

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-07978) VUID-VkCopyBufferToImageInfo2-dstImage-07978

If `dstImage` has a depth/stencil format, the `bufferOffset`
member of any element of `pRegions` **must** be a multiple of `4`

* 
[](#VUID-VkCopyBufferToImageInfo2-pRegions-06223) VUID-VkCopyBufferToImageInfo2-pRegions-06223

For each element of `pRegions` not containing
`VkCopyCommandTransformInfoQCOM` in its `pNext` chain,
`imageOffset.x` and (`imageExtent.width` + 
`imageOffset.x`) **must** both be greater than or equal to `0` and
less than or equal to the width of the specified `imageSubresource`
of `dstImage`

* 
[](#VUID-VkCopyBufferToImageInfo2-pRegions-06224) VUID-VkCopyBufferToImageInfo2-pRegions-06224

For each element of `pRegions` not containing
`VkCopyCommandTransformInfoQCOM` in its `pNext` chain,
`imageOffset.y` and (`imageExtent.height` + 
`imageOffset.y`) **must** both be greater than or equal to `0` and
less than or equal to the height of the specified `imageSubresource`
of `dstImage`

Valid Usage (Implicit)

* 
[](#VUID-VkCopyBufferToImageInfo2-sType-sType) VUID-VkCopyBufferToImageInfo2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_BUFFER_TO_IMAGE_INFO_2`

* 
[](#VUID-VkCopyBufferToImageInfo2-pNext-pNext) VUID-VkCopyBufferToImageInfo2-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkCopyBufferToImageInfo2-srcBuffer-parameter) VUID-VkCopyBufferToImageInfo2-srcBuffer-parameter

 `srcBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImage-parameter) VUID-VkCopyBufferToImageInfo2-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyBufferToImageInfo2-dstImageLayout-parameter) VUID-VkCopyBufferToImageInfo2-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyBufferToImageInfo2-pRegions-parameter) VUID-VkCopyBufferToImageInfo2-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkBufferImageCopy2](#VkBufferImageCopy2) structures

* 
[](#VUID-VkCopyBufferToImageInfo2-regionCount-arraylength) VUID-VkCopyBufferToImageInfo2-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkCopyBufferToImageInfo2-commonparent) VUID-VkCopyBufferToImageInfo2-commonparent

 Both of `dstImage`, and `srcBuffer` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

To copy data from an image object to a buffer object, call:

// Provided by VK_VERSION_1_3
void vkCmdCopyImageToBuffer2(
    VkCommandBuffer                             commandBuffer,
    const VkCopyImageToBufferInfo2*             pCopyImageToBufferInfo);

or the equivalent command

// Provided by VK_KHR_copy_commands2
void vkCmdCopyImageToBuffer2KHR(
    VkCommandBuffer                             commandBuffer,
    const VkCopyImageToBufferInfo2*             pCopyImageToBufferInfo);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`pCopyImageToBufferInfo` is a pointer to a
[VkCopyImageToBufferInfo2](#VkCopyImageToBufferInfo2) structure describing the copy parameters.

This command is functionally identical to [vkCmdCopyImageToBuffer](#vkCmdCopyImageToBuffer), but
includes extensible sub-structures that include `sType` and `pNext`
parameters, allowing them to be more easily extended.

Valid Usage

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-01831) VUID-vkCmdCopyImageToBuffer2-commandBuffer-01831

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-01832) VUID-vkCmdCopyImageToBuffer2-commandBuffer-01832

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be a protected buffer

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-01833) VUID-vkCmdCopyImageToBuffer2-commandBuffer-01833

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstBuffer` **must** not be an unprotected buffer

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-07746) VUID-vkCmdCopyImageToBuffer2-commandBuffer-07746

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT` or `VK_QUEUE_COMPUTE_BIT`, the
`bufferOffset` member of any element of `pCopyImageToBufferInfo->pRegions` **must** be a
multiple of `4`

* 
[](#VUID-vkCmdCopyImageToBuffer2-imageOffset-07747) VUID-vkCmdCopyImageToBuffer2-imageOffset-07747

The `imageOffset` and `imageExtent` members of each element of
`pCopyImageToBufferInfo->pRegions` **must** respect the image transfer granularity requirements
of `commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-10216) VUID-vkCmdCopyImageToBuffer2-commandBuffer-10216

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
`commandBuffer` was allocated from does not support
`VK_QUEUE_GRAPHICS_BIT`, for each element of `pCopyImageToBufferInfo->pRegions`, the
`aspectMask` member of `imageSubresource` **must** not be
`VK_IMAGE_ASPECT_DEPTH_BIT` or `VK_IMAGE_ASPECT_STENCIL_BIT`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-parameter) VUID-vkCmdCopyImageToBuffer2-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyImageToBuffer2-pCopyImageToBufferInfo-parameter) VUID-vkCmdCopyImageToBuffer2-pCopyImageToBufferInfo-parameter

 `pCopyImageToBufferInfo` **must** be a valid pointer to a valid [VkCopyImageToBufferInfo2](#VkCopyImageToBufferInfo2) structure

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-recording) VUID-vkCmdCopyImageToBuffer2-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyImageToBuffer2-commandBuffer-cmdpool) VUID-vkCmdCopyImageToBuffer2-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyImageToBuffer2-renderpass) VUID-vkCmdCopyImageToBuffer2-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyImageToBuffer2-videocoding) VUID-vkCmdCopyImageToBuffer2-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The `VkCopyImageToBufferInfo2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkCopyImageToBufferInfo2 {
    VkStructureType              sType;
    const void*                  pNext;
    VkImage                      srcImage;
    VkImageLayout                srcImageLayout;
    VkBuffer                     dstBuffer;
    uint32_t                     regionCount;
    const VkBufferImageCopy2*    pRegions;
} VkCopyImageToBufferInfo2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkCopyImageToBufferInfo2 VkCopyImageToBufferInfo2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the copy.

* 
`dstBuffer` is the destination buffer.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkBufferImageCopy2](#VkBufferImageCopy2)
structures specifying the regions to copy.

Valid Usage

* 
[](#VUID-VkCopyImageToBufferInfo2-pRegions-04566) VUID-VkCopyImageToBufferInfo2-pRegions-04566

The image region specified by each element of `pRegions`
that does not contain [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its
`pNext` chain
**must** be contained within the specified `imageSubresource` of
`srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2KHR-pRegions-04557) VUID-VkCopyImageToBufferInfo2KHR-pRegions-04557

If the image region specified by each element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, the
[rotated source region](#copies-buffers-images-rotation-addressing)
**must** be contained within `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2KHR-pRegions-04558) VUID-VkCopyImageToBufferInfo2KHR-pRegions-04558

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`srcImage` **must** have a 1x1x1 [texel    block extent](formats.html#formats-compatibility-classes)

* 
[](#VUID-VkCopyImageToBufferInfo2KHR-pRegions-06205) VUID-VkCopyImageToBufferInfo2KHR-pRegions-06205

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`srcImage` **must** be of type `VK_IMAGE_TYPE_2D`

* 
[](#VUID-VkCopyImageToBufferInfo2KHR-pRegions-06206) VUID-VkCopyImageToBufferInfo2KHR-pRegions-06206

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`srcImage` **must** not have a [multi-planar    format](formats.html#formats-multiplanar)

* 
[](#VUID-VkCopyImageToBufferInfo2-pRegions-00183) VUID-VkCopyImageToBufferInfo2-pRegions-00183

`dstBuffer` **must** be large enough to contain all buffer locations
that are accessed according to [Buffer    and Image Addressing](#copies-buffers-images-addressing), for each element of `pRegions`

* 
[](#VUID-VkCopyImageToBufferInfo2-pRegions-00184) VUID-VkCopyImageToBufferInfo2-pRegions-00184

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-00186) VUID-VkCopyImageToBufferInfo2-srcImage-00186

`srcImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-01998) VUID-VkCopyImageToBufferInfo2-srcImage-01998

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_SRC_BIT`

* 
[](#VUID-VkCopyImageToBufferInfo2-dstBuffer-00191) VUID-VkCopyImageToBufferInfo2-dstBuffer-00191

`dstBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-VkCopyImageToBufferInfo2-dstBuffer-00192) VUID-VkCopyImageToBufferInfo2-dstBuffer-00192

If `dstBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImageLayout-00189) VUID-VkCopyImageToBufferInfo2-srcImageLayout-00189

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImageLayout-01397) VUID-VkCopyImageToBufferInfo2-srcImageLayout-01397

`srcImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL`, or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07966) VUID-VkCopyImageToBufferInfo2-srcImage-07966

If `srcImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyImageToBufferInfo2-imageSubresource-07967) VUID-VkCopyImageToBufferInfo2-imageSubresource-07967

The `imageSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageToBufferInfo2-imageSubresource-07968) VUID-VkCopyImageToBufferInfo2-imageSubresource-07968

If `imageSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`imageSubresource.baseArrayLayer` + 
`imageSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07969) VUID-VkCopyImageToBufferInfo2-srcImage-07969

`srcImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07973) VUID-VkCopyImageToBufferInfo2-srcImage-07973

`srcImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07979) VUID-VkCopyImageToBufferInfo2-srcImage-07979

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `imageOffset.y` **must** be `0` and
`imageExtent.height` **must** be `1`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-09104) VUID-VkCopyImageToBufferInfo2-imageOffset-09104

For each element of `pRegions`, `imageOffset.z` and
(`imageExtent.depth` +  `imageOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `imageSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07980) VUID-VkCopyImageToBufferInfo2-srcImage-07980

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`imageOffset.z` **must** be `0` and `imageExtent.depth` **must**
be `1`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07274) VUID-VkCopyImageToBufferInfo2-srcImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`imageOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10051) VUID-VkCopyImageToBufferInfo2-imageOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `imageOffset.x`
does not equal the width of the subresource specified by
`imageSubresource`, `imageOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07275) VUID-VkCopyImageToBufferInfo2-srcImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`imageOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10052) VUID-VkCopyImageToBufferInfo2-imageOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `imageOffset.y`
does not equal the height of the subresource specified by
`imageSubresource`, `imageOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07276) VUID-VkCopyImageToBufferInfo2-srcImage-07276

For each element of `pRegions`, `imageOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-00207) VUID-VkCopyImageToBufferInfo2-srcImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `imageOffset.x` and `extent.width` does not equal
the width of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10053) VUID-VkCopyImageToBufferInfo2-imageOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`imageOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10054) VUID-VkCopyImageToBufferInfo2-imageOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10055) VUID-VkCopyImageToBufferInfo2-imageOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`imageOffset.x` and `extent.height` does not equal the width
of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-00208) VUID-VkCopyImageToBufferInfo2-srcImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `imageOffset.y` and `extent.height` does not equal
the height of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10056) VUID-VkCopyImageToBufferInfo2-imageOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`imageOffset.y` and `extent.width` does not equal the height
of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10057) VUID-VkCopyImageToBufferInfo2-imageOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-10058) VUID-VkCopyImageToBufferInfo2-imageOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`imageOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-00209) VUID-VkCopyImageToBufferInfo2-srcImage-00209

For each element of `pRegions`, if the sum of `imageOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageSubresource-09105) VUID-VkCopyImageToBufferInfo2-imageSubresource-09105

For each element of `pRegions`, `imageSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07981) VUID-VkCopyImageToBufferInfo2-srcImage-07981

If `srcImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`imageSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07983) VUID-VkCopyImageToBufferInfo2-srcImage-07983

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `imageSubresource.baseArrayLayer` **must**
be `0` and `imageSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyImageToBufferInfo2-bufferRowLength-09106) VUID-VkCopyImageToBufferInfo2-bufferRowLength-09106

For each element of `pRegions`, `bufferRowLength` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-bufferImageHeight-09107) VUID-VkCopyImageToBufferInfo2-bufferImageHeight-09107

For each element of `pRegions`, `bufferImageHeight` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-bufferRowLength-09108) VUID-VkCopyImageToBufferInfo2-bufferRowLength-09108

For each element of `pRegions`, `bufferRowLength` divided by
the [texel block extent width](formats.html#formats-compatibility-classes) and then
multiplied by the texel block size of `srcImage` **must** be less
than or equal to 231-1

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07975) VUID-VkCopyImageToBufferInfo2-srcImage-07975

If `srcImage` does not have either a depth/stencil format
or a [multi-planar format](formats.html#formats-multiplanar),
then for each element of `pRegions`, `bufferOffset` **must** be a
multiple of the [texel block size](formats.html#formats-compatibility-classes)

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07976) VUID-VkCopyImageToBufferInfo2-srcImage-07976

If `srcImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`, `bufferOffset`
**must** be a multiple of the element size of the compatible format for the
format and the `aspectMask` of the `imageSubresource` as defined
in [Compatible Formats of Planes of Multi-Planar Formats](formats.html#formats-compatible-planes)

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-07978) VUID-VkCopyImageToBufferInfo2-srcImage-07978

If `srcImage` has a depth/stencil format, the `bufferOffset`
member of any element of `pRegions` **must** be a multiple of `4`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-00197) VUID-VkCopyImageToBufferInfo2-imageOffset-00197

For each element of `pRegions` not containing
`VkCopyCommandTransformInfoQCOM` in its `pNext` chain,
`imageOffset.x` and (`imageExtent.width` + 
`imageOffset.x`) **must** both be greater than or equal to `0` and
less than or equal to the width of the specified `imageSubresource`
of `srcImage`

* 
[](#VUID-VkCopyImageToBufferInfo2-imageOffset-00198) VUID-VkCopyImageToBufferInfo2-imageOffset-00198

For each element of `pRegions` not containing
`VkCopyCommandTransformInfoQCOM` in its `pNext` chain,
`imageOffset.y` and (`imageExtent.height` + 
`imageOffset.y`) **must** both be greater than or equal to `0` and
less than or equal to the height of the specified `imageSubresource`
of `srcImage`

Valid Usage (Implicit)

* 
[](#VUID-VkCopyImageToBufferInfo2-sType-sType) VUID-VkCopyImageToBufferInfo2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_IMAGE_TO_BUFFER_INFO_2`

* 
[](#VUID-VkCopyImageToBufferInfo2-pNext-pNext) VUID-VkCopyImageToBufferInfo2-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImage-parameter) VUID-VkCopyImageToBufferInfo2-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyImageToBufferInfo2-srcImageLayout-parameter) VUID-VkCopyImageToBufferInfo2-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyImageToBufferInfo2-dstBuffer-parameter) VUID-VkCopyImageToBufferInfo2-dstBuffer-parameter

 `dstBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-VkCopyImageToBufferInfo2-pRegions-parameter) VUID-VkCopyImageToBufferInfo2-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkBufferImageCopy2](#VkBufferImageCopy2) structures

* 
[](#VUID-VkCopyImageToBufferInfo2-regionCount-arraylength) VUID-VkCopyImageToBufferInfo2-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkCopyImageToBufferInfo2-commonparent) VUID-VkCopyImageToBufferInfo2-commonparent

 Both of `dstBuffer`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

For both [vkCmdCopyBufferToImage2](#vkCmdCopyBufferToImage2) and [vkCmdCopyImageToBuffer2](#vkCmdCopyImageToBuffer2),
each element of `pRegions` is a structure defined as:

// Provided by VK_VERSION_1_3
typedef struct VkBufferImageCopy2 {
    VkStructureType             sType;
    const void*                 pNext;
    VkDeviceSize                bufferOffset;
    uint32_t                    bufferRowLength;
    uint32_t                    bufferImageHeight;
    VkImageSubresourceLayers    imageSubresource;
    VkOffset3D                  imageOffset;
    VkExtent3D                  imageExtent;
} VkBufferImageCopy2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkBufferImageCopy2 VkBufferImageCopy2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`bufferOffset` is the offset in bytes from the start of the buffer
object where the image data is copied from or to.

* 
`bufferRowLength` and `bufferImageHeight` specify in texels a
subregion of a larger two- or three-dimensional image in buffer memory,
and control the addressing calculations.
If either of these values is zero, that aspect of the buffer memory is
considered to be tightly packed according to the `imageExtent`.

* 
`imageSubresource` is a [VkImageSubresourceLayers](#VkImageSubresourceLayers) used to
specify the specific image subresources of the image used for the source
or destination image data.

* 
`imageOffset` selects the initial `x`, `y`, `z` offsets
in texels of the sub-region of the source or destination image data.

* 
`imageExtent` is the size in texels of the image to copy in
`width`, `height` and `depth`.

This structure is functionally identical to [VkBufferImageCopy](#VkBufferImageCopy), but
adds `sType` and `pNext` parameters, allowing it to be more easily
extended.

Valid Usage

* 
[](#VUID-VkBufferImageCopy2-bufferRowLength-09101) VUID-VkBufferImageCopy2-bufferRowLength-09101

`bufferRowLength` **must** be `0`, or greater than or equal to the
`width` member of `imageExtent`

* 
[](#VUID-VkBufferImageCopy2-bufferImageHeight-09102) VUID-VkBufferImageCopy2-bufferImageHeight-09102

`bufferImageHeight` **must** be `0`, or greater than or equal to the
`height` member of `imageExtent`

* 
[](#VUID-VkBufferImageCopy2-aspectMask-09103) VUID-VkBufferImageCopy2-aspectMask-09103

The `aspectMask` member of `imageSubresource` **must** only have a
single bit set

* 
[](#VUID-VkBufferImageCopy2-imageExtent-06659) VUID-VkBufferImageCopy2-imageExtent-06659

`imageExtent.width` **must** not be 0

* 
[](#VUID-VkBufferImageCopy2-imageExtent-06660) VUID-VkBufferImageCopy2-imageExtent-06660

`imageExtent.height` **must** not be 0

* 
[](#VUID-VkBufferImageCopy2-imageExtent-06661) VUID-VkBufferImageCopy2-imageExtent-06661

`imageExtent.depth` **must** not be 0

Valid Usage (Implicit)

* 
[](#VUID-VkBufferImageCopy2-sType-sType) VUID-VkBufferImageCopy2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_BUFFER_IMAGE_COPY_2`

* 
[](#VUID-VkBufferImageCopy2-pNext-pNext) VUID-VkBufferImageCopy2-pNext-pNext

 `pNext` **must** be `NULL` or a pointer to a valid instance of [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)

* 
[](#VUID-VkBufferImageCopy2-sType-unique) VUID-VkBufferImageCopy2-sType-unique

 The `sType` value of each structure in the `pNext` chain **must** be unique

* 
[](#VUID-VkBufferImageCopy2-imageSubresource-parameter) VUID-VkBufferImageCopy2-imageSubresource-parameter

 `imageSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

The `VkCopyCommandTransformInfoQCOM` structure is defined as:

// Provided by VK_QCOM_rotated_copy_commands
typedef struct VkCopyCommandTransformInfoQCOM {
    VkStructureType                  sType;
    const void*                      pNext;
    VkSurfaceTransformFlagBitsKHR    transform;
} VkCopyCommandTransformInfoQCOM;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`transform` is a [VkSurfaceTransformFlagBitsKHR](VK_KHR_surface/wsi.html#VkSurfaceTransformFlagBitsKHR) value
describing the transform to be applied.

Including this structure in the `pNext` chain of
[VkBufferImageCopy2](#VkBufferImageCopy2) defines a rotation to be performed when copying
between an image and a buffer.
Including this structure in the `pNext` chain of [VkBlitImageInfo2](#VkBlitImageInfo2)
defines a rotation to be performed when blitting between two images.
If this structure is not specified in either case, the implementation
behaves as if it was specified with a `transform` equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`.

Specifying a transform for a copy between an image and a buffer
[rotates the region accessed in the image around the offset](#copies-buffers-images-rotation-addressing).
Specifying a transform for a blit performs a similar transform as described
in [Image Blits with Scaling and Rotation](#copies-images-scaling-rotation).

Rotations other than `VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` **can** only
be specified for single-plane 2D images with a 1x1x1
[texel block extent](formats.html#formats-compatibility-classes).

Valid Usage

* 
[](#VUID-VkCopyCommandTransformInfoQCOM-transform-04560) VUID-VkCopyCommandTransformInfoQCOM-transform-04560

`transform` **must** be `VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`

Valid Usage (Implicit)

* 
[](#VUID-VkCopyCommandTransformInfoQCOM-sType-sType) VUID-VkCopyCommandTransformInfoQCOM-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_COMMAND_TRANSFORM_INFO_QCOM`

The following commands can be used to copy between host memory and images.
Bytes in host memory and texels in images are accessed as specified in
[Copying Data Between Buffers and Images](#copies-buffers-images), with
buffers replaced with host memory.

To copy data from host memory to an image object, call:

// Provided by VK_VERSION_1_4
VkResult vkCopyMemoryToImage(
    VkDevice                                    device,
    const VkCopyMemoryToImageInfo*              pCopyMemoryToImageInfo);

or the equivalent command

// Provided by VK_EXT_host_image_copy
VkResult vkCopyMemoryToImageEXT(
    VkDevice                                    device,
    const VkCopyMemoryToImageInfo*              pCopyMemoryToImageInfo);

* 
`device` is the device which owns
`pCopyMemoryToImageInfo->dstImage`.

* 
`pCopyMemoryToImageInfo` is a pointer to a
[VkCopyMemoryToImageInfo](#VkCopyMemoryToImageInfo) structure describing the copy parameters.

This command is functionally similar to [vkCmdCopyBufferToImage2](#vkCmdCopyBufferToImage2),
except it is executed on the host and reads from host memory instead of a
buffer.
The memory of `pCopyMemoryToImageInfo->dstImage` is accessed by the host
as if [coherent](memory.html#memory-coherent).

Valid Usage (Implicit)

* 
[](#VUID-vkCopyMemoryToImage-device-parameter) VUID-vkCopyMemoryToImage-device-parameter

 `device` **must** be a valid [VkDevice](devsandqueues.html#VkDevice) handle

* 
[](#VUID-vkCopyMemoryToImage-pCopyMemoryToImageInfo-parameter) VUID-vkCopyMemoryToImage-pCopyMemoryToImageInfo-parameter

 `pCopyMemoryToImageInfo` **must** be a valid pointer to a valid [VkCopyMemoryToImageInfo](#VkCopyMemoryToImageInfo) structure

Return Codes

[Success](fundamentals.html#fundamentals-successcodes)

* 
`VK_SUCCESS`

[Failure](fundamentals.html#fundamentals-errorcodes)

* 
`VK_ERROR_INITIALIZATION_FAILED`

* 
`VK_ERROR_OUT_OF_HOST_MEMORY`

* 
`VK_ERROR_OUT_OF_DEVICE_MEMORY`

* 
`VK_ERROR_MEMORY_MAP_FAILED`

The `VkCopyMemoryToImageInfo` structure is defined as:

// Provided by VK_VERSION_1_4
typedef struct VkCopyMemoryToImageInfo {
    VkStructureType               sType;
    const void*                   pNext;
    VkHostImageCopyFlags          flags;
    VkImage                       dstImage;
    VkImageLayout                 dstImageLayout;
    uint32_t                      regionCount;
    const VkMemoryToImageCopy*    pRegions;
} VkCopyMemoryToImageInfo;

or the equivalent

// Provided by VK_EXT_host_image_copy
typedef VkCopyMemoryToImageInfo VkCopyMemoryToImageInfoEXT;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`flags` is a bitmask of [VkHostImageCopyFlagBits](#VkHostImageCopyFlagBits) values
describing additional copy parameters.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the copy.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkMemoryToImageCopy](#VkMemoryToImageCopy)
structures specifying the regions to copy.

`vkCopyMemoryToImage` does not check whether the device memory
associated with `dstImage` is currently in use before performing the
copy.
The application **must** guarantee that any previously submitted command that
reads from or writes to the copy regions has completed before the host
performs the copy.

Copy regions for the image **must** be aligned to a multiple of the texel block
extent in each dimension, except at the edges of the image, where region
extents **must** match the edge of the image.

Valid Usage

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-09109) VUID-VkCopyMemoryToImageInfo-dstImage-09109

If `dstImage` is sparse then all memory ranges accessed by the
copy command **must** be bound as described in
[Binding Resource Memory](sparsemem.html#sparsememory-resource-binding)

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-09111) VUID-VkCopyMemoryToImageInfo-dstImage-09111

If the stencil aspect of `dstImage` is accessed, and
`dstImage` was not created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`dstImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-09112) VUID-VkCopyMemoryToImageInfo-dstImage-09112

If the stencil aspect of `dstImage` is accessed, and
`dstImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`dstImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-09113) VUID-VkCopyMemoryToImageInfo-dstImage-09113

If non-stencil aspects of `dstImage` are accessed,
`dstImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-09114) VUID-VkCopyMemoryToImageInfo-imageOffset-09114

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the `x`,
`y`, and `z` members of the `imageOffset` member of each
element of `pRegions` **must** be `0`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-09115) VUID-VkCopyMemoryToImageInfo-dstImage-09115

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the
`imageExtent` member of each element of `pRegions` **must** equal
the extents of `dstImage` identified by `imageSubresource`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07966) VUID-VkCopyMemoryToImageInfo-dstImage-07966

If `dstImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyMemoryToImageInfo-imageSubresource-07967) VUID-VkCopyMemoryToImageInfo-imageSubresource-07967

The `imageSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyMemoryToImageInfo-imageSubresource-07968) VUID-VkCopyMemoryToImageInfo-imageSubresource-07968

If `imageSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`imageSubresource.baseArrayLayer` + 
`imageSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07969) VUID-VkCopyMemoryToImageInfo-dstImage-07969

`dstImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageSubresource-07970) VUID-VkCopyMemoryToImageInfo-imageSubresource-07970

The image region specified by each element of `pRegions` **must** be
contained within the specified `imageSubresource` of
`dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageSubresource-07971) VUID-VkCopyMemoryToImageInfo-imageSubresource-07971

For each element of `pRegions`, `imageOffset.x` and
(`imageExtent.width` +  `imageOffset.x`) **must**
both be greater than or equal to `0` and less than or equal to the width
of the specified `imageSubresource` of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageSubresource-07972) VUID-VkCopyMemoryToImageInfo-imageSubresource-07972

For each element of `pRegions`, `imageOffset.y` and
(`imageExtent.height` +  `imageOffset.y`) **must**
both be greater than or equal to `0` and less than or equal to the
height of the specified `imageSubresource` of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07973) VUID-VkCopyMemoryToImageInfo-dstImage-07973

`dstImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07979) VUID-VkCopyMemoryToImageInfo-dstImage-07979

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `imageOffset.y` **must** be `0` and
`imageExtent.height` **must** be `1`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-09104) VUID-VkCopyMemoryToImageInfo-imageOffset-09104

For each element of `pRegions`, `imageOffset.z` and
(`imageExtent.depth` +  `imageOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `imageSubresource` of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07980) VUID-VkCopyMemoryToImageInfo-dstImage-07980

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`imageOffset.z` **must** be `0` and `imageExtent.depth` **must**
be `1`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07274) VUID-VkCopyMemoryToImageInfo-dstImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`imageOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10051) VUID-VkCopyMemoryToImageInfo-imageOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `imageOffset.x`
does not equal the width of the subresource specified by
`imageSubresource`, `imageOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07275) VUID-VkCopyMemoryToImageInfo-dstImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`imageOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10052) VUID-VkCopyMemoryToImageInfo-imageOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `imageOffset.y`
does not equal the height of the subresource specified by
`imageSubresource`, `imageOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07276) VUID-VkCopyMemoryToImageInfo-dstImage-07276

For each element of `pRegions`, `imageOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-00207) VUID-VkCopyMemoryToImageInfo-dstImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `imageOffset.x` and `extent.width` does not equal
the width of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10053) VUID-VkCopyMemoryToImageInfo-imageOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`imageOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10054) VUID-VkCopyMemoryToImageInfo-imageOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10055) VUID-VkCopyMemoryToImageInfo-imageOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`imageOffset.x` and `extent.height` does not equal the width
of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-00208) VUID-VkCopyMemoryToImageInfo-dstImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `imageOffset.y` and `extent.height` does not equal
the height of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10056) VUID-VkCopyMemoryToImageInfo-imageOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`imageOffset.y` and `extent.width` does not equal the height
of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10057) VUID-VkCopyMemoryToImageInfo-imageOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageOffset-10058) VUID-VkCopyMemoryToImageInfo-imageOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`imageOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-00209) VUID-VkCopyMemoryToImageInfo-dstImage-00209

For each element of `pRegions`, if the sum of `imageOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-imageSubresource-09105) VUID-VkCopyMemoryToImageInfo-imageSubresource-09105

For each element of `pRegions`, `imageSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07981) VUID-VkCopyMemoryToImageInfo-dstImage-07981

If `dstImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`imageSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-07983) VUID-VkCopyMemoryToImageInfo-dstImage-07983

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `imageSubresource.baseArrayLayer` **must**
be `0` and `imageSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyMemoryToImageInfo-memoryRowLength-09106) VUID-VkCopyMemoryToImageInfo-memoryRowLength-09106

For each element of `pRegions`, `memoryRowLength` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-memoryImageHeight-09107) VUID-VkCopyMemoryToImageInfo-memoryImageHeight-09107

For each element of `pRegions`, `memoryImageHeight` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyMemoryToImageInfo-memoryRowLength-09108) VUID-VkCopyMemoryToImageInfo-memoryRowLength-09108

For each element of `pRegions`, `memoryRowLength` divided by
the [texel block extent width](formats.html#formats-compatibility-classes) and then
multiplied by the texel block size of `dstImage` **must** be less
than or equal to 231-1

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImageLayout-09059) VUID-VkCopyMemoryToImageInfo-dstImageLayout-09059

`dstImageLayout` **must** specify the current layout of the image
subresources of `dstImage` specified in `pRegions`

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImageLayout-09060) VUID-VkCopyMemoryToImageInfo-dstImageLayout-09060

`dstImageLayout` **must** be one of the image layouts returned in
[VkPhysicalDeviceHostImageCopyProperties](limits.html#VkPhysicalDeviceHostImageCopyProperties)::`pCopyDstLayouts`

* 
[](#VUID-VkCopyMemoryToImageInfo-flags-09393) VUID-VkCopyMemoryToImageInfo-flags-09393

If `flags` includes `VK_HOST_IMAGE_COPY_MEMCPY`, for each region
in `pRegions`, `memoryRowLength` and `memoryImageHeight`
**must** both be 0

Valid Usage (Implicit)

* 
[](#VUID-VkCopyMemoryToImageInfo-sType-sType) VUID-VkCopyMemoryToImageInfo-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_MEMORY_TO_IMAGE_INFO`

* 
[](#VUID-VkCopyMemoryToImageInfo-pNext-pNext) VUID-VkCopyMemoryToImageInfo-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkCopyMemoryToImageInfo-flags-parameter) VUID-VkCopyMemoryToImageInfo-flags-parameter

 `flags` **must** be a valid combination of [VkHostImageCopyFlagBits](#VkHostImageCopyFlagBits) values

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImage-parameter) VUID-VkCopyMemoryToImageInfo-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyMemoryToImageInfo-dstImageLayout-parameter) VUID-VkCopyMemoryToImageInfo-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyMemoryToImageInfo-pRegions-parameter) VUID-VkCopyMemoryToImageInfo-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkMemoryToImageCopy](#VkMemoryToImageCopy) structures

* 
[](#VUID-VkCopyMemoryToImageInfo-regionCount-arraylength) VUID-VkCopyMemoryToImageInfo-regionCount-arraylength

 `regionCount` **must** be greater than `0`

Each element of [VkCopyMemoryToImageInfo](#VkCopyMemoryToImageInfo)::`pRegions` is a structure
defined as:

// Provided by VK_VERSION_1_4
typedef struct VkMemoryToImageCopy {
    VkStructureType             sType;
    const void*                 pNext;
    const void*                 pHostPointer;
    uint32_t                    memoryRowLength;
    uint32_t                    memoryImageHeight;
    VkImageSubresourceLayers    imageSubresource;
    VkOffset3D                  imageOffset;
    VkExtent3D                  imageExtent;
} VkMemoryToImageCopy;

or the equivalent

// Provided by VK_EXT_host_image_copy
typedef VkMemoryToImageCopy VkMemoryToImageCopyEXT;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`pHostPointer` is the host memory address which is the source of the
copy.

* 
`memoryRowLength` and `memoryImageHeight` specify in texels a
subregion of a larger two- or three-dimensional image in host memory,
and control the addressing calculations.
If either of these values is zero, that aspect of the host memory is
considered to be tightly packed according to the `imageExtent`.

* 
`imageSubresource` is a [VkImageSubresourceLayers](#VkImageSubresourceLayers) used to
specify the specific image subresources of the image used for the source
or destination image data.

* 
`imageOffset` selects the initial `x`, `y`, `z` offsets
in texels of the sub-region of the destination image data.

* 
`imageExtent` is the size in texels of the image to copy in
`width`, `height` and `depth`.

This structure is functionally similar to [VkBufferImageCopy2](#VkBufferImageCopy2), except
it defines host memory as the source of copy instead of a buffer.
In particular, the same data packing rules and restrictions as that
structure apply here as well.

Valid Usage

* 
[](#VUID-VkMemoryToImageCopy-pHostPointer-09061) VUID-VkMemoryToImageCopy-pHostPointer-09061

`pHostPointer` **must** point to memory that is large enough to contain
all memory locations that are accessed according to
[Buffer and Image Addressing](#copies-buffers-images-addressing), for
each element of `pRegions`

* 
[](#VUID-VkMemoryToImageCopy-pRegions-09062) VUID-VkMemoryToImageCopy-pRegions-09062

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-VkMemoryToImageCopy-memoryRowLength-09101) VUID-VkMemoryToImageCopy-memoryRowLength-09101

`memoryRowLength` **must** be `0`, or greater than or equal to the
`width` member of `imageExtent`

* 
[](#VUID-VkMemoryToImageCopy-memoryImageHeight-09102) VUID-VkMemoryToImageCopy-memoryImageHeight-09102

`memoryImageHeight` **must** be `0`, or greater than or equal to the
`height` member of `imageExtent`

* 
[](#VUID-VkMemoryToImageCopy-aspectMask-09103) VUID-VkMemoryToImageCopy-aspectMask-09103

The `aspectMask` member of `imageSubresource` **must** only have a
single bit set

* 
[](#VUID-VkMemoryToImageCopy-imageExtent-06659) VUID-VkMemoryToImageCopy-imageExtent-06659

`imageExtent.width` **must** not be 0

* 
[](#VUID-VkMemoryToImageCopy-imageExtent-06660) VUID-VkMemoryToImageCopy-imageExtent-06660

`imageExtent.height` **must** not be 0

* 
[](#VUID-VkMemoryToImageCopy-imageExtent-06661) VUID-VkMemoryToImageCopy-imageExtent-06661

`imageExtent.depth` **must** not be 0

Valid Usage (Implicit)

* 
[](#VUID-VkMemoryToImageCopy-sType-sType) VUID-VkMemoryToImageCopy-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_MEMORY_TO_IMAGE_COPY`

* 
[](#VUID-VkMemoryToImageCopy-pNext-pNext) VUID-VkMemoryToImageCopy-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkMemoryToImageCopy-pHostPointer-parameter) VUID-VkMemoryToImageCopy-pHostPointer-parameter

 `pHostPointer` **must** be a pointer value

* 
[](#VUID-VkMemoryToImageCopy-imageSubresource-parameter) VUID-VkMemoryToImageCopy-imageSubresource-parameter

 `imageSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

To copy data from an image object to host memory, call:

// Provided by VK_VERSION_1_4
VkResult vkCopyImageToMemory(
    VkDevice                                    device,
    const VkCopyImageToMemoryInfo*              pCopyImageToMemoryInfo);

or the equivalent command

// Provided by VK_EXT_host_image_copy
VkResult vkCopyImageToMemoryEXT(
    VkDevice                                    device,
    const VkCopyImageToMemoryInfo*              pCopyImageToMemoryInfo);

* 
`device` is the device which owns
`pCopyImageToMemoryInfo->srcImage`.

* 
`pCopyImageToMemoryInfo` is a pointer to a
[VkCopyImageToMemoryInfo](#VkCopyImageToMemoryInfo) structure describing the copy parameters.

This command is functionally similar to [vkCmdCopyImageToBuffer2](#vkCmdCopyImageToBuffer2),
except it is executed on the host and writes to host memory instead of a
buffer.
The memory of `pCopyImageToMemoryInfo->srcImage` is accessed by the host
as if [coherent](memory.html#memory-coherent).

Valid Usage (Implicit)

* 
[](#VUID-vkCopyImageToMemory-device-parameter) VUID-vkCopyImageToMemory-device-parameter

 `device` **must** be a valid [VkDevice](devsandqueues.html#VkDevice) handle

* 
[](#VUID-vkCopyImageToMemory-pCopyImageToMemoryInfo-parameter) VUID-vkCopyImageToMemory-pCopyImageToMemoryInfo-parameter

 `pCopyImageToMemoryInfo` **must** be a valid pointer to a valid [VkCopyImageToMemoryInfo](#VkCopyImageToMemoryInfo) structure

Return Codes

[Success](fundamentals.html#fundamentals-successcodes)

* 
`VK_SUCCESS`

[Failure](fundamentals.html#fundamentals-errorcodes)

* 
`VK_ERROR_INITIALIZATION_FAILED`

* 
`VK_ERROR_OUT_OF_HOST_MEMORY`

* 
`VK_ERROR_OUT_OF_DEVICE_MEMORY`

* 
`VK_ERROR_MEMORY_MAP_FAILED`

The `VkCopyImageToMemoryInfo` structure is defined as:

// Provided by VK_VERSION_1_4
typedef struct VkCopyImageToMemoryInfo {
    VkStructureType               sType;
    const void*                   pNext;
    VkHostImageCopyFlags          flags;
    VkImage                       srcImage;
    VkImageLayout                 srcImageLayout;
    uint32_t                      regionCount;
    const VkImageToMemoryCopy*    pRegions;
} VkCopyImageToMemoryInfo;

or the equivalent

// Provided by VK_EXT_host_image_copy
typedef VkCopyImageToMemoryInfo VkCopyImageToMemoryInfoEXT;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`flags` is a bitmask of [VkHostImageCopyFlagBits](#VkHostImageCopyFlagBits) values
describing additional copy parameters.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the copy.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkImageToMemoryCopy](#VkImageToMemoryCopy)
structures specifying the regions to copy.

`vkCopyImageToMemory` does not check whether the device memory
associated with `srcImage` is currently in use before performing the
copy.
The application **must** guarantee that any previously submitted command that
writes to the copy regions has completed before the host performs the copy.

Copy regions for the image **must** be aligned to a multiple of the texel block
extent in each dimension, except at the edges of the image, where region
extents **must** match the edge of the image.

Valid Usage

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-09109) VUID-VkCopyImageToMemoryInfo-srcImage-09109

If `srcImage` is sparse then all memory ranges accessed by the
copy command **must** be bound as described in
[Binding Resource Memory](sparsemem.html#sparsememory-resource-binding)

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-09111) VUID-VkCopyImageToMemoryInfo-srcImage-09111

If the stencil aspect of `srcImage` is accessed, and
`srcImage` was not created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`srcImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-09112) VUID-VkCopyImageToMemoryInfo-srcImage-09112

If the stencil aspect of `srcImage` is accessed, and
`srcImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`srcImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-09113) VUID-VkCopyImageToMemoryInfo-srcImage-09113

If non-stencil aspects of `srcImage` are accessed,
`srcImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-09114) VUID-VkCopyImageToMemoryInfo-imageOffset-09114

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the `x`,
`y`, and `z` members of the `imageOffset` member of each
element of `pRegions` **must** be `0`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-09115) VUID-VkCopyImageToMemoryInfo-srcImage-09115

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the
`imageExtent` member of each element of `pRegions` **must** equal
the extents of `srcImage` identified by `imageSubresource`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07966) VUID-VkCopyImageToMemoryInfo-srcImage-07966

If `srcImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyImageToMemoryInfo-imageSubresource-07967) VUID-VkCopyImageToMemoryInfo-imageSubresource-07967

The `imageSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageToMemoryInfo-imageSubresource-07968) VUID-VkCopyImageToMemoryInfo-imageSubresource-07968

If `imageSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`imageSubresource.baseArrayLayer` + 
`imageSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07969) VUID-VkCopyImageToMemoryInfo-srcImage-07969

`srcImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageSubresource-07970) VUID-VkCopyImageToMemoryInfo-imageSubresource-07970

The image region specified by each element of `pRegions` **must** be
contained within the specified `imageSubresource` of
`srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageSubresource-07971) VUID-VkCopyImageToMemoryInfo-imageSubresource-07971

For each element of `pRegions`, `imageOffset.x` and
(`imageExtent.width` +  `imageOffset.x`) **must**
both be greater than or equal to `0` and less than or equal to the width
of the specified `imageSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageSubresource-07972) VUID-VkCopyImageToMemoryInfo-imageSubresource-07972

For each element of `pRegions`, `imageOffset.y` and
(`imageExtent.height` +  `imageOffset.y`) **must**
both be greater than or equal to `0` and less than or equal to the
height of the specified `imageSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07973) VUID-VkCopyImageToMemoryInfo-srcImage-07973

`srcImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07979) VUID-VkCopyImageToMemoryInfo-srcImage-07979

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `imageOffset.y` **must** be `0` and
`imageExtent.height` **must** be `1`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-09104) VUID-VkCopyImageToMemoryInfo-imageOffset-09104

For each element of `pRegions`, `imageOffset.z` and
(`imageExtent.depth` +  `imageOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `imageSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07980) VUID-VkCopyImageToMemoryInfo-srcImage-07980

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`imageOffset.z` **must** be `0` and `imageExtent.depth` **must**
be `1`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07274) VUID-VkCopyImageToMemoryInfo-srcImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`imageOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10051) VUID-VkCopyImageToMemoryInfo-imageOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `imageOffset.x`
does not equal the width of the subresource specified by
`imageSubresource`, `imageOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07275) VUID-VkCopyImageToMemoryInfo-srcImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`imageOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10052) VUID-VkCopyImageToMemoryInfo-imageOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `imageOffset.y`
does not equal the height of the subresource specified by
`imageSubresource`, `imageOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07276) VUID-VkCopyImageToMemoryInfo-srcImage-07276

For each element of `pRegions`, `imageOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-00207) VUID-VkCopyImageToMemoryInfo-srcImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `imageOffset.x` and `extent.width` does not equal
the width of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10053) VUID-VkCopyImageToMemoryInfo-imageOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`imageOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10054) VUID-VkCopyImageToMemoryInfo-imageOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10055) VUID-VkCopyImageToMemoryInfo-imageOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`imageOffset.x` and `extent.height` does not equal the width
of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-00208) VUID-VkCopyImageToMemoryInfo-srcImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `imageOffset.y` and `extent.height` does not equal
the height of the subresource specified by `imageSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10056) VUID-VkCopyImageToMemoryInfo-imageOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`imageOffset.y` and `extent.width` does not equal the height
of the subresource specified by `imageSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10057) VUID-VkCopyImageToMemoryInfo-imageOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`imageOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageOffset-10058) VUID-VkCopyImageToMemoryInfo-imageOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`imageOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-00209) VUID-VkCopyImageToMemoryInfo-srcImage-00209

For each element of `pRegions`, if the sum of `imageOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-imageSubresource-09105) VUID-VkCopyImageToMemoryInfo-imageSubresource-09105

For each element of `pRegions`, `imageSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07981) VUID-VkCopyImageToMemoryInfo-srcImage-07981

If `srcImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`imageSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-07983) VUID-VkCopyImageToMemoryInfo-srcImage-07983

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `imageSubresource.baseArrayLayer` **must**
be `0` and `imageSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyImageToMemoryInfo-memoryRowLength-09106) VUID-VkCopyImageToMemoryInfo-memoryRowLength-09106

For each element of `pRegions`, `memoryRowLength` **must** be a
multiple of the [texel block extent    width](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-memoryImageHeight-09107) VUID-VkCopyImageToMemoryInfo-memoryImageHeight-09107

For each element of `pRegions`, `memoryImageHeight` **must** be a
multiple of the [texel block extent    height](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToMemoryInfo-memoryRowLength-09108) VUID-VkCopyImageToMemoryInfo-memoryRowLength-09108

For each element of `pRegions`, `memoryRowLength` divided by
the [texel block extent width](formats.html#formats-compatibility-classes) and then
multiplied by the texel block size of `srcImage` **must** be less
than or equal to 231-1

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImageLayout-09064) VUID-VkCopyImageToMemoryInfo-srcImageLayout-09064

`srcImageLayout` **must** specify the current layout of the image
subresources of `srcImage` specified in `pRegions`

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImageLayout-09065) VUID-VkCopyImageToMemoryInfo-srcImageLayout-09065

`srcImageLayout` **must** be one of the image layouts returned in
[VkPhysicalDeviceHostImageCopyProperties](limits.html#VkPhysicalDeviceHostImageCopyProperties)::`pCopySrcLayouts`

* 
[](#VUID-VkCopyImageToMemoryInfo-flags-09394) VUID-VkCopyImageToMemoryInfo-flags-09394

If `flags` includes `VK_HOST_IMAGE_COPY_MEMCPY`, for each region
in `pRegions`, `memoryRowLength` and `memoryImageHeight`
**must** both be 0

Valid Usage (Implicit)

* 
[](#VUID-VkCopyImageToMemoryInfo-sType-sType) VUID-VkCopyImageToMemoryInfo-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_IMAGE_TO_MEMORY_INFO`

* 
[](#VUID-VkCopyImageToMemoryInfo-pNext-pNext) VUID-VkCopyImageToMemoryInfo-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkCopyImageToMemoryInfo-flags-parameter) VUID-VkCopyImageToMemoryInfo-flags-parameter

 `flags` **must** be a valid combination of [VkHostImageCopyFlagBits](#VkHostImageCopyFlagBits) values

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImage-parameter) VUID-VkCopyImageToMemoryInfo-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyImageToMemoryInfo-srcImageLayout-parameter) VUID-VkCopyImageToMemoryInfo-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyImageToMemoryInfo-pRegions-parameter) VUID-VkCopyImageToMemoryInfo-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageToMemoryCopy](#VkImageToMemoryCopy) structures

* 
[](#VUID-VkCopyImageToMemoryInfo-regionCount-arraylength) VUID-VkCopyImageToMemoryInfo-regionCount-arraylength

 `regionCount` **must** be greater than `0`

Each element of [VkCopyImageToMemoryInfo](#VkCopyImageToMemoryInfo)::`pRegions` is a structure
defined as:

// Provided by VK_VERSION_1_4
typedef struct VkImageToMemoryCopy {
    VkStructureType             sType;
    const void*                 pNext;
    void*                       pHostPointer;
    uint32_t                    memoryRowLength;
    uint32_t                    memoryImageHeight;
    VkImageSubresourceLayers    imageSubresource;
    VkOffset3D                  imageOffset;
    VkExtent3D                  imageExtent;
} VkImageToMemoryCopy;

or the equivalent

// Provided by VK_EXT_host_image_copy
typedef VkImageToMemoryCopy VkImageToMemoryCopyEXT;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`pHostPointer` is the host memory address which is the destination
of the copy.

* 
`memoryRowLength` and `memoryImageHeight` specify in texels a
subregion of a larger two- or three-dimensional image in host memory,
and control the addressing calculations.
If either of these values is zero, that aspect of the host memory is
considered to be tightly packed according to the `imageExtent`.

* 
`imageSubresource` is a [VkImageSubresourceLayers](#VkImageSubresourceLayers) used to
specify the specific image subresources of the image used for the source
or destination image data.

* 
`imageOffset` selects the initial `x`, `y`, `z` offsets
in texels of the sub-region of the source image data.

* 
`imageExtent` is the size in texels of the image to copy in
`width`, `height` and `depth`.

This structure is functionally similar to [VkBufferImageCopy2](#VkBufferImageCopy2), except
it defines host memory as the target of copy instead of a buffer.
In particular, the same data packing rules and restrictions as that
structure apply here as well.

Valid Usage

* 
[](#VUID-VkImageToMemoryCopy-pHostPointer-09066) VUID-VkImageToMemoryCopy-pHostPointer-09066

`pHostPointer` **must** point to memory that is large enough to contain
all memory locations that are accessed according to
[Buffer and Image Addressing](#copies-buffers-images-addressing), for
each element of `pRegions`

* 
[](#VUID-VkImageToMemoryCopy-pRegions-09067) VUID-VkImageToMemoryCopy-pRegions-09067

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-VkImageToMemoryCopy-memoryRowLength-09101) VUID-VkImageToMemoryCopy-memoryRowLength-09101

`memoryRowLength` **must** be `0`, or greater than or equal to the
`width` member of `imageExtent`

* 
[](#VUID-VkImageToMemoryCopy-memoryImageHeight-09102) VUID-VkImageToMemoryCopy-memoryImageHeight-09102

`memoryImageHeight` **must** be `0`, or greater than or equal to the
`height` member of `imageExtent`

* 
[](#VUID-VkImageToMemoryCopy-aspectMask-09103) VUID-VkImageToMemoryCopy-aspectMask-09103

The `aspectMask` member of `imageSubresource` **must** only have a
single bit set

* 
[](#VUID-VkImageToMemoryCopy-imageExtent-06659) VUID-VkImageToMemoryCopy-imageExtent-06659

`imageExtent.width` **must** not be 0

* 
[](#VUID-VkImageToMemoryCopy-imageExtent-06660) VUID-VkImageToMemoryCopy-imageExtent-06660

`imageExtent.height` **must** not be 0

* 
[](#VUID-VkImageToMemoryCopy-imageExtent-06661) VUID-VkImageToMemoryCopy-imageExtent-06661

`imageExtent.depth` **must** not be 0

Valid Usage (Implicit)

* 
[](#VUID-VkImageToMemoryCopy-sType-sType) VUID-VkImageToMemoryCopy-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_IMAGE_TO_MEMORY_COPY`

* 
[](#VUID-VkImageToMemoryCopy-pNext-pNext) VUID-VkImageToMemoryCopy-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkImageToMemoryCopy-pHostPointer-parameter) VUID-VkImageToMemoryCopy-pHostPointer-parameter

 `pHostPointer` **must** be a pointer value

* 
[](#VUID-VkImageToMemoryCopy-imageSubresource-parameter) VUID-VkImageToMemoryCopy-imageSubresource-parameter

 `imageSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

Bits which **can** be set in [VkCopyMemoryToImageInfo](#VkCopyMemoryToImageInfo)::`flags`,
[VkCopyImageToMemoryInfo](#VkCopyImageToMemoryInfo)::`flags`, and
[VkCopyImageToImageInfo](#VkCopyImageToImageInfo)::`flags`, specifying additional copy
parameters are:

// Provided by VK_VERSION_1_4
typedef enum VkHostImageCopyFlagBits {
    VK_HOST_IMAGE_COPY_MEMCPY = 0x00000001,
  // Provided by VK_EXT_host_image_copy
    VK_HOST_IMAGE_COPY_MEMCPY_EXT = VK_HOST_IMAGE_COPY_MEMCPY,
} VkHostImageCopyFlagBits;

or the equivalent

// Provided by VK_EXT_host_image_copy
typedef VkHostImageCopyFlagBits VkHostImageCopyFlagBitsEXT;

* 
`VK_HOST_IMAGE_COPY_MEMCPY` specifies that no memory layout
swizzling is to be applied during data copy.
For copies between memory and images, this flag indicates that image
data in host memory is swizzled in exactly the same way as the image
data on the device.
Using this flag indicates that the implementations **may** use a simple
memory copy to transfer the data between the host memory and the device
memory.
The format of the swizzled data in host memory is platform dependent and
is not defined in this specification.

// Provided by VK_VERSION_1_4
typedef VkFlags VkHostImageCopyFlags;

or the equivalent

// Provided by VK_EXT_host_image_copy
typedef VkHostImageCopyFlags VkHostImageCopyFlagsEXT;

`VkHostImageCopyFlags` is a bitmask type for setting a mask of zero or
more [VkHostImageCopyFlagBits](#VkHostImageCopyFlagBits).

To copy data from an image object to another image object using the host,
call:

// Provided by VK_VERSION_1_4
VkResult vkCopyImageToImage(
    VkDevice                                    device,
    const VkCopyImageToImageInfo*               pCopyImageToImageInfo);

or the equivalent command

// Provided by VK_EXT_host_image_copy
VkResult vkCopyImageToImageEXT(
    VkDevice                                    device,
    const VkCopyImageToImageInfo*               pCopyImageToImageInfo);

* 
`device` is the device which owns
`pCopyImageToImageInfo->srcImage` and
`pCopyImageToImageInfo->dstImage`.

* 
`pCopyImageToImageInfo` is a pointer to a
[VkCopyImageToImageInfo](#VkCopyImageToImageInfo) structure describing the copy parameters.

This command is functionally similar to [vkCmdCopyImage2](#vkCmdCopyImage2), except it is
executed on the host.
The memory of `pCopyImageToImageInfo->srcImage` and
`pCopyImageToImageInfo->dstImage` is accessed by the host as if
[coherent](memory.html#memory-coherent).

Valid Usage (Implicit)

* 
[](#VUID-vkCopyImageToImage-device-parameter) VUID-vkCopyImageToImage-device-parameter

 `device` **must** be a valid [VkDevice](devsandqueues.html#VkDevice) handle

* 
[](#VUID-vkCopyImageToImage-pCopyImageToImageInfo-parameter) VUID-vkCopyImageToImage-pCopyImageToImageInfo-parameter

 `pCopyImageToImageInfo` **must** be a valid pointer to a valid [VkCopyImageToImageInfo](#VkCopyImageToImageInfo) structure

Return Codes

[Success](fundamentals.html#fundamentals-successcodes)

* 
`VK_SUCCESS`

[Failure](fundamentals.html#fundamentals-errorcodes)

* 
`VK_ERROR_INITIALIZATION_FAILED`

* 
`VK_ERROR_OUT_OF_HOST_MEMORY`

* 
`VK_ERROR_OUT_OF_DEVICE_MEMORY`

* 
`VK_ERROR_MEMORY_MAP_FAILED`

The `VkCopyImageToImageInfo` structure is defined as:

// Provided by VK_VERSION_1_4
typedef struct VkCopyImageToImageInfo {
    VkStructureType         sType;
    const void*             pNext;
    VkHostImageCopyFlags    flags;
    VkImage                 srcImage;
    VkImageLayout           srcImageLayout;
    VkImage                 dstImage;
    VkImageLayout           dstImageLayout;
    uint32_t                regionCount;
    const VkImageCopy2*     pRegions;
} VkCopyImageToImageInfo;

or the equivalent

// Provided by VK_EXT_host_image_copy
typedef VkCopyImageToImageInfo VkCopyImageToImageInfoEXT;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`flags` is a bitmask of [VkHostImageCopyFlagBits](#VkHostImageCopyFlagBits) values
describing additional copy parameters.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the copy.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the copy.

* 
`regionCount` is the number of regions to copy.

* 
`pRegions` is a pointer to an array of [VkImageCopy2](#VkImageCopy2) structures
specifying the regions to copy.

`vkCopyImageToImage` does not check whether the device memory associated
with `srcImage` or `dstImage` is currently in use before performing
the copy.
The application **must** guarantee that any previously submitted command that
writes to the copy regions has completed before the host performs the copy.

Valid Usage

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-09069) VUID-VkCopyImageToImageInfo-srcImage-09069

`srcImage` and `dstImage` **must** have been created with identical
image creation parameters

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-09109) VUID-VkCopyImageToImageInfo-srcImage-09109

If `srcImage` is sparse then all memory ranges accessed by the
copy command **must** be bound as described in
[Binding Resource Memory](sparsemem.html#sparsememory-resource-binding)

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-09111) VUID-VkCopyImageToImageInfo-srcImage-09111

If the stencil aspect of `srcImage` is accessed, and
`srcImage` was not created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`srcImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-09112) VUID-VkCopyImageToImageInfo-srcImage-09112

If the stencil aspect of `srcImage` is accessed, and
`srcImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`srcImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-09113) VUID-VkCopyImageToImageInfo-srcImage-09113

If non-stencil aspects of `srcImage` are accessed,
`srcImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-09114) VUID-VkCopyImageToImageInfo-srcOffset-09114

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the `x`,
`y`, and `z` members of the `srcOffset` member of each
element of `pRegions` **must** be `0`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-09115) VUID-VkCopyImageToImageInfo-srcImage-09115

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the
`extent` member of each element of `pRegions` **must** equal
the extents of `srcImage` identified by `srcSubresource`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07966) VUID-VkCopyImageToImageInfo-srcImage-07966

If `srcImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyImageToImageInfo-srcSubresource-07967) VUID-VkCopyImageToImageInfo-srcSubresource-07967

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageToImageInfo-srcSubresource-07968) VUID-VkCopyImageToImageInfo-srcSubresource-07968

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07969) VUID-VkCopyImageToImageInfo-srcImage-07969

`srcImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkCopyImageToImageInfo-srcSubresource-07970) VUID-VkCopyImageToImageInfo-srcSubresource-07970

The image region specified by each element of `pRegions` **must** be
contained within the specified `srcSubresource` of
`srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcSubresource-07971) VUID-VkCopyImageToImageInfo-srcSubresource-07971

For each element of `pRegions`, `srcOffset.x` and
(`extent.width` +  `srcOffset.x`) **must**
both be greater than or equal to `0` and less than or equal to the width
of the specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcSubresource-07972) VUID-VkCopyImageToImageInfo-srcSubresource-07972

For each element of `pRegions`, `srcOffset.y` and
(`extent.height` +  `srcOffset.y`) **must**
both be greater than or equal to `0` and less than or equal to the
height of the specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07979) VUID-VkCopyImageToImageInfo-srcImage-07979

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-09104) VUID-VkCopyImageToImageInfo-srcOffset-09104

For each element of `pRegions`, `srcOffset.z` and
(`extent.depth` +  `srcOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07980) VUID-VkCopyImageToImageInfo-srcImage-07980

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`srcOffset.z` **must** be `0` and `extent.depth` **must**
be `1`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07274) VUID-VkCopyImageToImageInfo-srcImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`srcOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10051) VUID-VkCopyImageToImageInfo-srcOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `srcOffset.x`
does not equal the width of the subresource specified by
`srcSubresource`, `srcOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07275) VUID-VkCopyImageToImageInfo-srcImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`srcOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10052) VUID-VkCopyImageToImageInfo-srcOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `srcOffset.y`
does not equal the height of the subresource specified by
`srcSubresource`, `srcOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07276) VUID-VkCopyImageToImageInfo-srcImage-07276

For each element of `pRegions`, `srcOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-00207) VUID-VkCopyImageToImageInfo-srcImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `srcOffset.x` and `extent.width` does not equal
the width of the subresource specified by `srcSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10053) VUID-VkCopyImageToImageInfo-srcOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`srcOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10054) VUID-VkCopyImageToImageInfo-srcOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`srcOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10055) VUID-VkCopyImageToImageInfo-srcOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`srcOffset.x` and `extent.height` does not equal the width
of the subresource specified by `srcSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-00208) VUID-VkCopyImageToImageInfo-srcImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `srcOffset.y` and `extent.height` does not equal
the height of the subresource specified by `srcSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10056) VUID-VkCopyImageToImageInfo-srcOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`srcOffset.y` and `extent.width` does not equal the height
of the subresource specified by `srcSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10057) VUID-VkCopyImageToImageInfo-srcOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`srcOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcOffset-10058) VUID-VkCopyImageToImageInfo-srcOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`srcOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-00209) VUID-VkCopyImageToImageInfo-srcImage-00209

For each element of `pRegions`, if the sum of `srcOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcSubresource-09105) VUID-VkCopyImageToImageInfo-srcSubresource-09105

For each element of `pRegions`, `srcSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07981) VUID-VkCopyImageToImageInfo-srcImage-07981

If `srcImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`srcSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-07983) VUID-VkCopyImageToImageInfo-srcImage-07983

If `srcImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `srcSubresource.baseArrayLayer` **must**
be `0` and `srcSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-09109) VUID-VkCopyImageToImageInfo-dstImage-09109

If `dstImage` is sparse then all memory ranges accessed by the
copy command **must** be bound as described in
[Binding Resource Memory](sparsemem.html#sparsememory-resource-binding)

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-09111) VUID-VkCopyImageToImageInfo-dstImage-09111

If the stencil aspect of `dstImage` is accessed, and
`dstImage` was not created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`dstImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-09112) VUID-VkCopyImageToImageInfo-dstImage-09112

If the stencil aspect of `dstImage` is accessed, and
`dstImage` was created with
[separate stencil usage](resources.html#VkImageStencilUsageCreateInfo),
`dstImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageStencilUsageCreateInfo](resources.html#VkImageStencilUsageCreateInfo)::`stencilUsage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-09113) VUID-VkCopyImageToImageInfo-dstImage-09113

If non-stencil aspects of `dstImage` are accessed,
`dstImage` **must** have been created with
`VK_IMAGE_USAGE_HOST_TRANSFER_BIT` set in
[VkImageCreateInfo](resources.html#VkImageCreateInfo)::`usage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-09114) VUID-VkCopyImageToImageInfo-dstOffset-09114

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the `x`,
`y`, and `z` members of the `dstOffset` member of each
element of `pRegions` **must** be `0`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-09115) VUID-VkCopyImageToImageInfo-dstImage-09115

If `flags` contains `VK_HOST_IMAGE_COPY_MEMCPY`, the
`extent` member of each element of `pRegions` **must** equal
the extents of `dstImage` identified by `dstSubresource`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07966) VUID-VkCopyImageToImageInfo-dstImage-07966

If `dstImage` is non-sparse then the image
or the specified *disjoint* plane
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-VkCopyImageToImageInfo-dstSubresource-07967) VUID-VkCopyImageToImageInfo-dstSubresource-07967

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyImageToImageInfo-dstSubresource-07968) VUID-VkCopyImageToImageInfo-dstSubresource-07968

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions`
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07969) VUID-VkCopyImageToImageInfo-dstImage-07969

`dstImage` **must** not have been created with `flags`
containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkCopyImageToImageInfo-dstSubresource-07970) VUID-VkCopyImageToImageInfo-dstSubresource-07970

The image region specified by each element of `pRegions` **must** be
contained within the specified `dstSubresource` of
`dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstSubresource-07971) VUID-VkCopyImageToImageInfo-dstSubresource-07971

For each element of `pRegions`, `dstOffset.x` and
(`extent.width` +  `dstOffset.x`) **must**
both be greater than or equal to `0` and less than or equal to the width
of the specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstSubresource-07972) VUID-VkCopyImageToImageInfo-dstSubresource-07972

For each element of `pRegions`, `dstOffset.y` and
(`extent.height` +  `dstOffset.y`) **must**
both be greater than or equal to `0` and less than or equal to the
height of the specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07979) VUID-VkCopyImageToImageInfo-dstImage-07979

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-09104) VUID-VkCopyImageToImageInfo-dstOffset-09104

For each element of `pRegions`, `dstOffset.z` and
(`extent.depth` +  `dstOffset.z`) **must**
both be greater than or equal to `0` and less than or equal to the depth
of the specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07980) VUID-VkCopyImageToImageInfo-dstImage-07980

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`dstOffset.z` **must** be `0` and `extent.depth` **must**
be `1`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07274) VUID-VkCopyImageToImageInfo-dstImage-07274

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`,
`dstOffset.x` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10051) VUID-VkCopyImageToImageInfo-dstOffset-10051

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, and `dstOffset.x`
does not equal the width of the subresource specified by
`dstSubresource`, `dstOffset.x` **must** be a multiple of
the [texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07275) VUID-VkCopyImageToImageInfo-dstImage-07275

For each element of `pRegions`,
if [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`,
`dstOffset.y` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10052) VUID-VkCopyImageToImageInfo-dstOffset-10052

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR` or
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, and `dstOffset.y`
does not equal the height of the subresource specified by
`dstSubresource`, `dstOffset.y` **must** be a multiple of
the [texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07276) VUID-VkCopyImageToImageInfo-dstImage-07276

For each element of `pRegions`, `dstOffset.z` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-00207) VUID-VkCopyImageToImageInfo-dstImage-00207

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`,
the sum of `dstOffset.x` and `extent.width` does not equal
the width of the subresource specified by `dstSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10053) VUID-VkCopyImageToImageInfo-dstOffset-10053

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the difference of
`dstOffset.x` and `extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10054) VUID-VkCopyImageToImageInfo-dstOffset-10054

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`dstOffset.x` and `extent.width` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10055) VUID-VkCopyImageToImageInfo-dstOffset-10055

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the sum of
`dstOffset.x` and `extent.height` does not equal the width
of the subresource specified by `dstSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent width](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-00208) VUID-VkCopyImageToImageInfo-dstImage-00208

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR`, and
the sum of `dstOffset.y` and `extent.height` does not equal
the height of the subresource specified by `dstSubresource`,
`extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10056) VUID-VkCopyImageToImageInfo-dstOffset-10056

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR`, the sum of
`dstOffset.y` and `extent.width` does not equal the height
of the subresource specified by `dstSubresource`,
`extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10057) VUID-VkCopyImageToImageInfo-dstOffset-10057

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR`, the difference of
`dstOffset.y` and `extent.height` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstOffset-10058) VUID-VkCopyImageToImageInfo-dstOffset-10058

For each element of `pRegions`, if
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)::`transform` is equal to
`VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR`, the difference of
`dstOffset.y` and `extent.width` **must** be a multiple of the
[texel block extent height](formats.html#formats-compatibility-classes) of the
[VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-00209) VUID-VkCopyImageToImageInfo-dstImage-00209

For each element of `pRegions`, if the sum of `dstOffset.z`
and `extent.depth` does not equal the depth of the subresource
specified by `srcSubresource`, `extent.depth` **must** be a
multiple of the [texel block extent    depth](formats.html#formats-compatibility-classes) of the [VkFormat](formats.html#VkFormat) of `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstSubresource-09105) VUID-VkCopyImageToImageInfo-dstSubresource-09105

For each element of `pRegions`, `dstSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07981) VUID-VkCopyImageToImageInfo-dstImage-07981

If `dstImage` has a [multi-planar    format](formats.html#formats-multiplanar), then for each element of `pRegions`,
`dstSubresource.aspectMask` **must** be a single valid
[multi-planar aspect mask](formats.html#formats-multiplanar-image-aspect) bit

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-07983) VUID-VkCopyImageToImageInfo-dstImage-07983

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, for each
element of `pRegions`, `dstSubresource.baseArrayLayer` **must**
be `0` and `dstSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkCopyImageToImageInfo-srcImageLayout-09070) VUID-VkCopyImageToImageInfo-srcImageLayout-09070

`srcImageLayout` **must** specify the current layout of the image
subresources of `srcImage` specified in `pRegions`

* 
[](#VUID-VkCopyImageToImageInfo-dstImageLayout-09071) VUID-VkCopyImageToImageInfo-dstImageLayout-09071

`dstImageLayout` **must** specify the current layout of the image
subresources of `dstImage` specified in `pRegions`

* 
[](#VUID-VkCopyImageToImageInfo-srcImageLayout-09072) VUID-VkCopyImageToImageInfo-srcImageLayout-09072

`srcImageLayout` **must** be one of the image layouts returned in
[VkPhysicalDeviceHostImageCopyProperties](limits.html#VkPhysicalDeviceHostImageCopyProperties)::`pCopySrcLayouts`

* 
[](#VUID-VkCopyImageToImageInfo-dstImageLayout-09073) VUID-VkCopyImageToImageInfo-dstImageLayout-09073

`dstImageLayout` **must** be one of the image layouts returned in
[VkPhysicalDeviceHostImageCopyProperties](limits.html#VkPhysicalDeviceHostImageCopyProperties)::`pCopyDstLayouts`

Valid Usage (Implicit)

* 
[](#VUID-VkCopyImageToImageInfo-sType-sType) VUID-VkCopyImageToImageInfo-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_COPY_IMAGE_TO_IMAGE_INFO`

* 
[](#VUID-VkCopyImageToImageInfo-pNext-pNext) VUID-VkCopyImageToImageInfo-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkCopyImageToImageInfo-flags-parameter) VUID-VkCopyImageToImageInfo-flags-parameter

 `flags` **must** be a valid combination of [VkHostImageCopyFlagBits](#VkHostImageCopyFlagBits) values

* 
[](#VUID-VkCopyImageToImageInfo-srcImage-parameter) VUID-VkCopyImageToImageInfo-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyImageToImageInfo-srcImageLayout-parameter) VUID-VkCopyImageToImageInfo-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyImageToImageInfo-dstImage-parameter) VUID-VkCopyImageToImageInfo-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkCopyImageToImageInfo-dstImageLayout-parameter) VUID-VkCopyImageToImageInfo-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkCopyImageToImageInfo-pRegions-parameter) VUID-VkCopyImageToImageInfo-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageCopy2](#VkImageCopy2) structures

* 
[](#VUID-VkCopyImageToImageInfo-regionCount-arraylength) VUID-VkCopyImageToImageInfo-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkCopyImageToImageInfo-commonparent) VUID-VkCopyImageToImageInfo-commonparent

 Both of `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

An application can use indirect copies when the copy parameters are not
known during the command buffer creation time.

To copy data between two memory regions by specifying copy parameters
indirectly in a buffer, call:

// Provided by VK_NV_copy_memory_indirect
void vkCmdCopyMemoryIndirectNV(
    VkCommandBuffer                             commandBuffer,
    VkDeviceAddress                             copyBufferAddress,
    uint32_t                                    copyCount,
    uint32_t                                    stride);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`copyBufferAddress` is the buffer address specifying the copy
parameters.
This buffer is laid out in memory as an array of
[VkCopyMemoryIndirectCommandNV](#VkCopyMemoryIndirectCommandNV) structures.

* 
`copyCount` is the number of copies to execute, and can be zero.

* 
`stride` is the stride in bytes between successive sets of copy
parameters.

Each region read from `copyBufferAddress` is copied from the source
region to the specified destination region.
The results are **undefined** if any of the source and destination regions
overlap in memory.

Valid Usage

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-None-07653) VUID-vkCmdCopyMemoryIndirectNV-None-07653

The [`indirectCopy`](features.html#features-indirectCopy) feature **must** be
enabled

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-copyBufferAddress-07654) VUID-vkCmdCopyMemoryIndirectNV-copyBufferAddress-07654

`copyBufferAddress` **must** be 4 byte aligned

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-stride-07655) VUID-vkCmdCopyMemoryIndirectNV-stride-07655

`stride` **must** be a multiple of `4` and **must** be greater than or
equal to sizeof(`VkCopyMemoryIndirectCommandNV`)

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-07656) VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-07656

The [VkCommandPool](cmdbuffers.html#VkCommandPool) that `commandBuffer` was allocated from
**must** support at least one of the
[VkPhysicalDeviceCopyMemoryIndirectPropertiesNV](limits.html#VkPhysicalDeviceCopyMemoryIndirectPropertiesNV)::`supportedQueues`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-parameter) VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-recording) VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-cmdpool) VUID-vkCmdCopyMemoryIndirectNV-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-renderpass) VUID-vkCmdCopyMemoryIndirectNV-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdCopyMemoryIndirectNV-videocoding) VUID-vkCmdCopyMemoryIndirectNV-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The structure describing source and destination memory regions,
`VkCopyMemoryIndirectCommandNV` is defined as:

// Provided by VK_NV_copy_memory_indirect
typedef struct VkCopyMemoryIndirectCommandNV {
    VkDeviceAddress    srcAddress;
    VkDeviceAddress    dstAddress;
    VkDeviceSize       size;
} VkCopyMemoryIndirectCommandNV;

* 
`srcAddress` is the starting address of the source device memory to
copy from.

* 
`dstAddress` is the starting address of the destination device
memory to copy to.

* 
`size` is the size of the copy in bytes.

Valid Usage

* 
[](#VUID-VkCopyMemoryIndirectCommandNV-srcAddress-07657) VUID-VkCopyMemoryIndirectCommandNV-srcAddress-07657

The `srcAddress` **must** be 4 byte aligned

* 
[](#VUID-VkCopyMemoryIndirectCommandNV-dstAddress-07658) VUID-VkCopyMemoryIndirectCommandNV-dstAddress-07658

The `dstAddress` **must** be 4 byte aligned

* 
[](#VUID-VkCopyMemoryIndirectCommandNV-size-07659) VUID-VkCopyMemoryIndirectCommandNV-size-07659

The `size` **must** be 4 byte aligned

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
[VkCopyMemoryToImageIndirectCommandNV](#VkCopyMemoryToImageIndirectCommandNV) structures.

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
`copyCount` of [VkImageSubresourceLayers](#VkImageSubresourceLayers) used to specify the
specific image subresource of the destination image data for that copy.

Each region in `copyBufferAddress` is copied from the source memory
region to an image region in the destination image.
If the destination image is of type `VK_IMAGE_TYPE_3D`, the starting
slice and number of slices to copy are specified in
`pImageSubresources->baseArrayLayer` and
`pImageSubresources->layerCount` respectively.
The copy **must** be performed on a queue that supports indirect copy
operations, see [VkPhysicalDeviceCopyMemoryIndirectPropertiesNV](limits.html#VkPhysicalDeviceCopyMemoryIndirectPropertiesNV).

Valid Usage

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-None-07660) VUID-vkCmdCopyMemoryToImageIndirectNV-None-07660

The [`indirectCopy`](features.html#features-indirectCopy) feature **must** be
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
`mipLevels` specified in [VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage`
was created

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-layerCount-08764) VUID-vkCmdCopyMemoryToImageIndirectNV-layerCount-08764

If `layerCount` is not `VK_REMAINING_ARRAY_LAYERS`, the
specified `baseArrayLayer` +  `layerCount` of each region
**must** be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-imageOffset-07672) VUID-vkCmdCopyMemoryToImageIndirectNV-imageOffset-07672

The `imageOffset` and `imageExtent` members of each region **must**
respect the image transfer granularity requirements of
`commandBuffer`’s command pool’s queue family, as described in
[VkQueueFamilyProperties](devsandqueues.html#VkQueueFamilyProperties)

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07673) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-07673

`dstImage` **must** not have been created with `flags` containing
`VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-07674) VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-07674

If the queue family used to create the [VkCommandPool](cmdbuffers.html#VkCommandPool) which
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

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-pImageSubresources-parameter) VUID-vkCmdCopyMemoryToImageIndirectNV-pImageSubresources-parameter

 `pImageSubresources` **must** be a valid pointer to an array of `copyCount` valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structures

* 
[](#VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-recording) VUID-vkCmdCopyMemoryToImageIndirectNV-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

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

 Both of `commandBuffer`, and `dstImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Transfer

Graphics

Compute
Action

The `VkCopyMemoryToImageIndirectCommandNV` is defined as:

// Provided by VK_NV_copy_memory_indirect
typedef struct VkCopyMemoryToImageIndirectCommandNV {
    VkDeviceAddress             srcAddress;
    uint32_t                    bufferRowLength;
    uint32_t                    bufferImageHeight;
    VkImageSubresourceLayers    imageSubresource;
    VkOffset3D                  imageOffset;
    VkExtent3D                  imageExtent;
} VkCopyMemoryToImageIndirectCommandNV;

* 
`srcAddress` is the starting address of the source device memory to
copy from.

* 
`bufferRowLength` and `bufferImageHeight` specify in texels a
subregion of a larger two- or three-dimensional image in buffer memory,
and control the addressing calculations.
If either of these values is zero, that aspect of the buffer memory is
considered to be tightly packed according to the `imageExtent`.

* 
`imageSubresource` is a [VkImageSubresourceLayers](#VkImageSubresourceLayers) used to
specify the specific image subresources of the image used for the
destination image data, which **must** match the values specified in
`pImageSubresources` parameter of
[vkCmdCopyMemoryToImageIndirectNV](#vkCmdCopyMemoryToImageIndirectNV) during command recording.

* 
`imageOffset` selects the initial `x`, `y`, `z` offsets
in texels of the sub-region of the destination image data.

* 
`imageExtent` is the size in texels of the destination image in
`width`, `height` and `depth`.

Valid Usage

* 
[](#VUID-VkCopyMemoryToImageIndirectCommandNV-srcAddress-07678) VUID-VkCopyMemoryToImageIndirectCommandNV-srcAddress-07678

The `srcAddress` **must** be 4 byte aligned

* 
[](#VUID-VkCopyMemoryToImageIndirectCommandNV-bufferRowLength-07679) VUID-VkCopyMemoryToImageIndirectCommandNV-bufferRowLength-07679

`bufferRowLength` **must** be `0`, or greater than or equal to the
`width` member of `imageExtent`

* 
[](#VUID-VkCopyMemoryToImageIndirectCommandNV-bufferImageHeight-07680) VUID-VkCopyMemoryToImageIndirectCommandNV-bufferImageHeight-07680

`bufferImageHeight` **must** be `0`, or greater than or equal to the
`height` member of `imageExtent`

* 
[](#VUID-VkCopyMemoryToImageIndirectCommandNV-imageOffset-07681) VUID-VkCopyMemoryToImageIndirectCommandNV-imageOffset-07681

`imageOffset` **must** specify a valid offset in the destination image

* 
[](#VUID-VkCopyMemoryToImageIndirectCommandNV-imageExtent-07682) VUID-VkCopyMemoryToImageIndirectCommandNV-imageExtent-07682

`imageExtent` **must** specify a valid region in the destination image
and can be `0`

Valid Usage (Implicit)

* 
[](#VUID-VkCopyMemoryToImageIndirectCommandNV-imageSubresource-parameter) VUID-VkCopyMemoryToImageIndirectCommandNV-imageSubresource-parameter

 `imageSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

To copy regions of a source image into a destination image, potentially
performing format conversion, arbitrary scaling, and filtering, call:

// Provided by VK_VERSION_1_0
void vkCmdBlitImage(
    VkCommandBuffer                             commandBuffer,
    VkImage                                     srcImage,
    VkImageLayout                               srcImageLayout,
    VkImage                                     dstImage,
    VkImageLayout                               dstImageLayout,
    uint32_t                                    regionCount,
    const VkImageBlit*                          pRegions,
    VkFilter                                    filter);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the blit.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the blit.

* 
`regionCount` is the number of regions to blit.

* 
`pRegions` is a pointer to an array of [VkImageBlit](#VkImageBlit) structures
specifying the regions to blit.

* 
`filter` is a [VkFilter](samplers.html#VkFilter) specifying the filter to apply if the
blits require scaling.

`vkCmdBlitImage` **must** not be used for multisampled source or
destination images.
Use [vkCmdResolveImage](#vkCmdResolveImage) for this purpose.

As the sizes of the source and destination extents **can** differ in any
dimension, texels in the source extent are scaled and filtered to the
destination extent.
Scaling occurs via the following operations:

* 
For each destination texel, the integer coordinate of that texel is
converted to an unnormalized texture coordinate, using the effective
inverse of the equations described in
[unnormalized to integer    conversion](textures.html#textures-unnormalized-to-integer):

ubase = i +  ½

vbase = j +  ½

wbase = k +  ½

* 
These base coordinates are then offset by the first destination offset:

uoffset = ubase - xdst0

voffset = vbase - ydst0

woffset = wbase - zdst0

aoffset = a - `baseArrayCount`dst

* 
The scale is determined from the source and destination regions, and
applied to the offset coordinates:

scaleu = (xsrc1 - xsrc0) / (xdst1 - xdst0)

scalev = (ysrc1 - ysrc0) / (ydst1 - ydst0)

scalew = (zsrc1 - zsrc0) / (zdst1 - zdst0)

uscaled = uoffset × scaleu

vscaled = voffset × scalev

wscaled = woffset × scalew

* 
Finally the source offset is added to the scaled coordinates, to
determine the final unnormalized coordinates used to sample from
`srcImage`:

u = uscaled +  xsrc0

v = vscaled +  ysrc0

w = wscaled +  zsrc0

q = `mipLevel`

a = aoffset +  `baseArrayCount`src

These coordinates are used to sample from the source image, as described in
[Image Operations chapter](textures.html#textures), with the filter mode equal to that
of `filter`, a mipmap mode of `VK_SAMPLER_MIPMAP_MODE_NEAREST` and
an address mode of `VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`.
Implementations **must** clamp at the edge of the source image, and **may**
additionally clamp to the edge of the source region.

Blits are done layer by layer starting with the `baseArrayLayer` member
of `srcSubresource` for the source and `dstSubresource` for the
destination.
`layerCount` layers are blitted to the destination image.

When blitting 3D textures, slices in the destination region bounded by
`dstOffsets`[0].z and `dstOffsets`[1].z are sampled from slices in
the source region bounded by `srcOffsets`[0].z and
`srcOffsets`[1].z.
If the `filter` parameter is `VK_FILTER_LINEAR` then the value
sampled from the source image is taken by doing linear filtering using the
interpolated **z** coordinate represented by **w** in the previous equations.
If the `filter` parameter is `VK_FILTER_NEAREST` then the value
sampled from the source image is taken from the single nearest slice, with
an implementation-dependent arithmetic rounding mode.

The following filtering and conversion rules apply:

* 
Integer formats **can** only be converted to other integer formats with the
same signedness.

* 
No format conversion is supported between depth/stencil images.
The formats **must** match.

* 
Format conversions on unorm, snorm, scaled and packed float formats of
the copied aspect of the image are performed by first converting the
pixels to float values.

* 
For sRGB source formats, nonlinear RGB values are converted to linear
representation prior to filtering.

* 
After filtering, the float values are first clamped and then cast to the
destination image format.
In case of sRGB destination format, linear RGB values are converted to
nonlinear representation before writing the pixel to the image.

Signed and unsigned integers are converted by first clamping to the
representable range of the destination format, then casting the value.

Valid Usage

* 
[](#VUID-vkCmdBlitImage-commandBuffer-01834) VUID-vkCmdBlitImage-commandBuffer-01834

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdBlitImage-commandBuffer-01835) VUID-vkCmdBlitImage-commandBuffer-01835

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdBlitImage-commandBuffer-01836) VUID-vkCmdBlitImage-commandBuffer-01836

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

* 
[](#VUID-vkCmdBlitImage-pRegions-00215) VUID-vkCmdBlitImage-pRegions-00215

The source region specified by each element of `pRegions` **must** be a
region that is contained within `srcImage`

* 
[](#VUID-vkCmdBlitImage-pRegions-00216) VUID-vkCmdBlitImage-pRegions-00216

The destination region specified by each element of `pRegions` **must**
be a region that is contained within `dstImage`

* 
[](#VUID-vkCmdBlitImage-pRegions-00217) VUID-vkCmdBlitImage-pRegions-00217

The union of all destination regions, specified by the elements of
`pRegions`, **must** not overlap in memory with any texel that **may** be
sampled during the blit operation

* 
[](#VUID-vkCmdBlitImage-srcImage-01999) VUID-vkCmdBlitImage-srcImage-01999

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_BLIT_SRC_BIT`

* 
[](#VUID-vkCmdBlitImage-srcImage-06421) VUID-vkCmdBlitImage-srcImage-06421

`srcImage` **must** not use a
[format that requires a    sampler Y′CBCR conversion](formats.html#formats-requiring-sampler-ycbcr-conversion)

* 
[](#VUID-vkCmdBlitImage-srcImage-00219) VUID-vkCmdBlitImage-srcImage-00219

`srcImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-vkCmdBlitImage-srcImage-00220) VUID-vkCmdBlitImage-srcImage-00220

If `srcImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdBlitImage-srcImageLayout-00221) VUID-vkCmdBlitImage-srcImageLayout-00221

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdBlitImage-srcImageLayout-01398) VUID-vkCmdBlitImage-srcImageLayout-01398

`srcImageLayout` **must** be `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdBlitImage-srcImage-09459) VUID-vkCmdBlitImage-srcImage-09459

If `srcImage` and `dstImage` are the same, and an elements of
`pRegions` contains the `srcSubresource` and
`dstSubresource` with matching `mipLevel` and overlapping array
layers, then the `srcImageLayout` and `dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_GENERAL`
or `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`

* 
[](#VUID-vkCmdBlitImage-dstImage-02000) VUID-vkCmdBlitImage-dstImage-02000

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_BLIT_DST_BIT`

* 
[](#VUID-vkCmdBlitImage-dstImage-06422) VUID-vkCmdBlitImage-dstImage-06422

`dstImage` **must** not use a
[format that requires a    sampler Y′CBCR conversion](formats.html#formats-requiring-sampler-ycbcr-conversion)

* 
[](#VUID-vkCmdBlitImage-dstImage-00224) VUID-vkCmdBlitImage-dstImage-00224

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdBlitImage-dstImage-00225) VUID-vkCmdBlitImage-dstImage-00225

If `dstImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdBlitImage-dstImageLayout-00226) VUID-vkCmdBlitImage-dstImageLayout-00226

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdBlitImage-dstImageLayout-01399) VUID-vkCmdBlitImage-dstImageLayout-01399

`dstImageLayout` **must** be `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdBlitImage-srcImage-00229) VUID-vkCmdBlitImage-srcImage-00229

If either of `srcImage` or `dstImage` was created with a signed
integer [VkFormat](formats.html#VkFormat), the other **must** also have been created with a
signed integer [VkFormat](formats.html#VkFormat)

* 
[](#VUID-vkCmdBlitImage-srcImage-00230) VUID-vkCmdBlitImage-srcImage-00230

If either of `srcImage` or `dstImage` was created with an
unsigned integer [VkFormat](formats.html#VkFormat), the other **must** also have been created
with an unsigned integer [VkFormat](formats.html#VkFormat)

* 
[](#VUID-vkCmdBlitImage-srcImage-00231) VUID-vkCmdBlitImage-srcImage-00231

If either of `srcImage` or `dstImage` was created with a
depth/stencil format, the other **must** have exactly the same format

* 
[](#VUID-vkCmdBlitImage-srcImage-00232) VUID-vkCmdBlitImage-srcImage-00232

If `srcImage` was created with a depth/stencil format, `filter`
**must** be `VK_FILTER_NEAREST`

* 
[](#VUID-vkCmdBlitImage-srcImage-00233) VUID-vkCmdBlitImage-srcImage-00233

`srcImage` **must** have been created with a `samples` value of
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-vkCmdBlitImage-dstImage-00234) VUID-vkCmdBlitImage-dstImage-00234

`dstImage` **must** have been created with a `samples` value of
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-vkCmdBlitImage-filter-02001) VUID-vkCmdBlitImage-filter-02001

If `filter` is `VK_FILTER_LINEAR`, then the
[format features](resources.html#resources-image-format-features) of `srcImage`
**must** contain `VK_FORMAT_FEATURE_SAMPLED_IMAGE_FILTER_LINEAR_BIT`

* 
[](#VUID-vkCmdBlitImage-filter-02002) VUID-vkCmdBlitImage-filter-02002

If `filter` is `VK_FILTER_CUBIC_EXT`, then the
[format features](resources.html#resources-image-format-features) of `srcImage`
**must** contain `VK_FORMAT_FEATURE_SAMPLED_IMAGE_FILTER_CUBIC_BIT_EXT`

* 
[](#VUID-vkCmdBlitImage-filter-00237) VUID-vkCmdBlitImage-filter-00237

If `filter` is `VK_FILTER_CUBIC_EXT`, `srcImage` **must** be of
type `VK_IMAGE_TYPE_2D`

* 
[](#VUID-vkCmdBlitImage-srcSubresource-01705) VUID-vkCmdBlitImage-srcSubresource-01705

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdBlitImage-dstSubresource-01706) VUID-vkCmdBlitImage-dstSubresource-01706

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdBlitImage-srcSubresource-01707) VUID-vkCmdBlitImage-srcSubresource-01707

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdBlitImage-dstSubresource-01708) VUID-vkCmdBlitImage-dstSubresource-01708

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdBlitImage-dstImage-02545) VUID-vkCmdBlitImage-dstImage-02545

`dstImage` and `srcImage` **must** not have been created with
`flags` containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-vkCmdBlitImage-maintenance8-10207) VUID-vkCmdBlitImage-maintenance8-10207

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled
and `srcImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcSubresource.baseArrayLayer` **must** be
`0`, and `srcSubresource.layerCount` and
`dstSubresource.layerCount` **must** each be `1`

* 
[](#VUID-vkCmdBlitImage-maintenance8-10208) VUID-vkCmdBlitImage-maintenance8-10208

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled
and `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstSubresource.baseArrayLayer` **must** be
`0`, and `srcSubresource.layerCount` and
`dstSubresource.layerCount` **must** each be `1`

* 
[](#VUID-vkCmdBlitImage-maintenance8-10579) VUID-vkCmdBlitImage-maintenance8-10579

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled,
`dstImage` is `VK_IMAGE_TYPE_3D`, and `srcImage` is not of
type `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
the absolute difference of the `z` member of each member of
`dstOffsets` **must** equal `srcSubresource.layerCount`

* 
[](#VUID-vkCmdBlitImage-maintenance8-10580) VUID-vkCmdBlitImage-maintenance8-10580

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled,
`srcImage` is `VK_IMAGE_TYPE_3D`, and `dstImage` is not of
type `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
the absolute difference of the `z` member of each member of
`srcOffsets` **must** equal `dstSubresource.layerCount`

* 
[](#VUID-vkCmdBlitImage-srcImage-00240) VUID-vkCmdBlitImage-srcImage-00240

    If
the [`maintenance8`](features.html#features-maintenance8) feature is not enabled and
    either `srcImage` or `dstImage` is of type
    `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
    `srcSubresource.baseArrayLayer` and
    `dstSubresource.baseArrayLayer` **must** each be `0`, and
    `srcSubresource.layerCount` and `dstSubresource.layerCount`
    **must** each be `1`

* 
[](#VUID-vkCmdBlitImage-aspectMask-00241) VUID-vkCmdBlitImage-aspectMask-00241

For each element of `pRegions`, `srcSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-vkCmdBlitImage-aspectMask-00242) VUID-vkCmdBlitImage-aspectMask-00242

For each element of `pRegions`, `dstSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-vkCmdBlitImage-srcOffset-00243) VUID-vkCmdBlitImage-srcOffset-00243

For each element of `pRegions`, `srcOffsets`[0].x and
`srcOffsets`[1].x **must** both be greater than or equal to `0` and
less than or equal to the width of the specified `srcSubresource` of
`srcImage`

* 
[](#VUID-vkCmdBlitImage-srcOffset-00244) VUID-vkCmdBlitImage-srcOffset-00244

For each element of `pRegions`, `srcOffsets`[0].y and
`srcOffsets`[1].y **must** both be greater than or equal to `0` and
less than or equal to the height of the specified `srcSubresource`
of `srcImage`

* 
[](#VUID-vkCmdBlitImage-srcImage-00245) VUID-vkCmdBlitImage-srcImage-00245

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffsets`[0].y **must** be `0` and
`srcOffsets`[1].y **must** be `1`

* 
[](#VUID-vkCmdBlitImage-srcOffset-00246) VUID-vkCmdBlitImage-srcOffset-00246

For each element of `pRegions`, `srcOffsets`[0].z and
`srcOffsets`[1].z **must** both be greater than or equal to `0` and
less than or equal to the depth of the specified `srcSubresource` of
`srcImage`

* 
[](#VUID-vkCmdBlitImage-srcImage-00247) VUID-vkCmdBlitImage-srcImage-00247

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`srcOffsets`[0].z **must** be `0` and `srcOffsets`[1].z **must** be
`1`

* 
[](#VUID-vkCmdBlitImage-dstOffset-00248) VUID-vkCmdBlitImage-dstOffset-00248

For each element of `pRegions`, `dstOffsets`[0].x and
`dstOffsets`[1].x **must** both be greater than or equal to `0` and
less than or equal to the width of the specified `dstSubresource` of
`dstImage`

* 
[](#VUID-vkCmdBlitImage-dstOffset-00249) VUID-vkCmdBlitImage-dstOffset-00249

For each element of `pRegions`, `dstOffsets`[0].y and
`dstOffsets`[1].y **must** both be greater than or equal to `0` and
less than or equal to the height of the specified `dstSubresource`
of `dstImage`

* 
[](#VUID-vkCmdBlitImage-dstImage-00250) VUID-vkCmdBlitImage-dstImage-00250

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffsets`[0].y **must** be `0` and
`dstOffsets`[1].y **must** be `1`

* 
[](#VUID-vkCmdBlitImage-dstOffset-00251) VUID-vkCmdBlitImage-dstOffset-00251

For each element of `pRegions`, `dstOffsets`[0].z and
`dstOffsets`[1].z **must** both be greater than or equal to `0` and
less than or equal to the depth of the specified `dstSubresource` of
`dstImage`

* 
[](#VUID-vkCmdBlitImage-dstImage-00252) VUID-vkCmdBlitImage-dstImage-00252

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`dstOffsets`[0].z **must** be `0` and `dstOffsets`[1].z **must** be
`1`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdBlitImage-commandBuffer-parameter) VUID-vkCmdBlitImage-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdBlitImage-srcImage-parameter) VUID-vkCmdBlitImage-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdBlitImage-srcImageLayout-parameter) VUID-vkCmdBlitImage-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdBlitImage-dstImage-parameter) VUID-vkCmdBlitImage-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdBlitImage-dstImageLayout-parameter) VUID-vkCmdBlitImage-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdBlitImage-pRegions-parameter) VUID-vkCmdBlitImage-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageBlit](#VkImageBlit) structures

* 
[](#VUID-vkCmdBlitImage-filter-parameter) VUID-vkCmdBlitImage-filter-parameter

 `filter` **must** be a valid [VkFilter](samplers.html#VkFilter) value

* 
[](#VUID-vkCmdBlitImage-commandBuffer-recording) VUID-vkCmdBlitImage-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdBlitImage-commandBuffer-cmdpool) VUID-vkCmdBlitImage-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics operations

* 
[](#VUID-vkCmdBlitImage-renderpass) VUID-vkCmdBlitImage-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdBlitImage-videocoding) VUID-vkCmdBlitImage-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdBlitImage-regionCount-arraylength) VUID-vkCmdBlitImage-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-vkCmdBlitImage-commonparent) VUID-vkCmdBlitImage-commonparent

 Each of `commandBuffer`, `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Graphics
Action

The `VkImageBlit` structure is defined as:

// Provided by VK_VERSION_1_0
typedef struct VkImageBlit {
    VkImageSubresourceLayers    srcSubresource;
    VkOffset3D                  srcOffsets[2];
    VkImageSubresourceLayers    dstSubresource;
    VkOffset3D                  dstOffsets[2];
} VkImageBlit;

* 
`srcSubresource` is the subresource to blit from.

* 
`srcOffsets` is a pointer to an array of two [VkOffset3D](fundamentals.html#VkOffset3D)
structures specifying the bounds of the source region within
`srcSubresource`.

* 
`dstSubresource` is the subresource to blit into.

* 
`dstOffsets` is a pointer to an array of two [VkOffset3D](fundamentals.html#VkOffset3D)
structures specifying the bounds of the destination region within
`dstSubresource`.

For each element of the `pRegions` array, a blit operation is performed
for the specified source and destination regions.

Valid Usage

* 
[](#VUID-VkImageBlit-aspectMask-00238) VUID-VkImageBlit-aspectMask-00238

The `aspectMask` member of `srcSubresource` and
`dstSubresource` **must** match

* 
[](#VUID-VkImageBlit-layerCount-08800) VUID-VkImageBlit-layerCount-08800

If neither of the `layerCount` members of `srcSubresource` or
`dstSubresource` are `VK_REMAINING_ARRAY_LAYERS`, the
`layerCount` members of `srcSubresource` or `dstSubresource`
**must** match

* 
[](#VUID-VkImageBlit-layerCount-08801) VUID-VkImageBlit-layerCount-08801

If one of the `layerCount` members of `srcSubresource` or
`dstSubresource` is `VK_REMAINING_ARRAY_LAYERS`, the other
member **must** be either `VK_REMAINING_ARRAY_LAYERS` or equal to the
`arrayLayers` member of the [VkImageCreateInfo](resources.html#VkImageCreateInfo) used to create
the image minus `baseArrayLayer`

Valid Usage (Implicit)

* 
[](#VUID-VkImageBlit-srcSubresource-parameter) VUID-VkImageBlit-srcSubresource-parameter

 `srcSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

* 
[](#VUID-VkImageBlit-dstSubresource-parameter) VUID-VkImageBlit-dstSubresource-parameter

 `dstSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

A more extensible version of the blit image command is defined below.

To copy regions of a source image into a destination image, potentially
performing format conversion, arbitrary scaling, and filtering, call:

// Provided by VK_VERSION_1_3
void vkCmdBlitImage2(
    VkCommandBuffer                             commandBuffer,
    const VkBlitImageInfo2*                     pBlitImageInfo);

or the equivalent command

// Provided by VK_KHR_copy_commands2
void vkCmdBlitImage2KHR(
    VkCommandBuffer                             commandBuffer,
    const VkBlitImageInfo2*                     pBlitImageInfo);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`pBlitImageInfo` is a pointer to a [VkBlitImageInfo2](#VkBlitImageInfo2) structure
describing the blit parameters.

This command is functionally identical to [vkCmdBlitImage](#vkCmdBlitImage), but includes
extensible sub-structures that include `sType` and `pNext`
parameters, allowing them to be more easily extended.

Valid Usage

* 
[](#VUID-vkCmdBlitImage2-commandBuffer-01834) VUID-vkCmdBlitImage2-commandBuffer-01834

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdBlitImage2-commandBuffer-01835) VUID-vkCmdBlitImage2-commandBuffer-01835

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdBlitImage2-commandBuffer-01836) VUID-vkCmdBlitImage2-commandBuffer-01836

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

Valid Usage (Implicit)

* 
[](#VUID-vkCmdBlitImage2-commandBuffer-parameter) VUID-vkCmdBlitImage2-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdBlitImage2-pBlitImageInfo-parameter) VUID-vkCmdBlitImage2-pBlitImageInfo-parameter

 `pBlitImageInfo` **must** be a valid pointer to a valid [VkBlitImageInfo2](#VkBlitImageInfo2) structure

* 
[](#VUID-vkCmdBlitImage2-commandBuffer-recording) VUID-vkCmdBlitImage2-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdBlitImage2-commandBuffer-cmdpool) VUID-vkCmdBlitImage2-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics operations

* 
[](#VUID-vkCmdBlitImage2-renderpass) VUID-vkCmdBlitImage2-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdBlitImage2-videocoding) VUID-vkCmdBlitImage2-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Graphics
Action

The `VkBlitImageInfo2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkBlitImageInfo2 {
    VkStructureType        sType;
    const void*            pNext;
    VkImage                srcImage;
    VkImageLayout          srcImageLayout;
    VkImage                dstImage;
    VkImageLayout          dstImageLayout;
    uint32_t               regionCount;
    const VkImageBlit2*    pRegions;
    VkFilter               filter;
} VkBlitImageInfo2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkBlitImageInfo2 VkBlitImageInfo2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the blit.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the blit.

* 
`regionCount` is the number of regions to blit.

* 
`pRegions` is a pointer to an array of [VkImageBlit2](#VkImageBlit2) structures
specifying the regions to blit.

* 
`filter` is a [VkFilter](samplers.html#VkFilter) specifying the filter to apply if the
blits require scaling.

Valid Usage

* 
[](#VUID-VkBlitImageInfo2-pRegions-00215) VUID-VkBlitImageInfo2-pRegions-00215

The source region specified by each element of `pRegions` **must** be a
region that is contained within `srcImage`

* 
[](#VUID-VkBlitImageInfo2-pRegions-00216) VUID-VkBlitImageInfo2-pRegions-00216

The destination region specified by each element of `pRegions` **must**
be a region that is contained within `dstImage`

* 
[](#VUID-VkBlitImageInfo2-pRegions-00217) VUID-VkBlitImageInfo2-pRegions-00217

The union of all destination regions, specified by the elements of
`pRegions`, **must** not overlap in memory with any texel that **may** be
sampled during the blit operation

* 
[](#VUID-VkBlitImageInfo2-srcImage-01999) VUID-VkBlitImageInfo2-srcImage-01999

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_BLIT_SRC_BIT`

* 
[](#VUID-VkBlitImageInfo2-srcImage-06421) VUID-VkBlitImageInfo2-srcImage-06421

`srcImage` **must** not use a
[format that requires a    sampler Y′CBCR conversion](formats.html#formats-requiring-sampler-ycbcr-conversion)

* 
[](#VUID-VkBlitImageInfo2-srcImage-00219) VUID-VkBlitImageInfo2-srcImage-00219

`srcImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-VkBlitImageInfo2-srcImage-00220) VUID-VkBlitImageInfo2-srcImage-00220

If `srcImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-VkBlitImageInfo2-srcImageLayout-00221) VUID-VkBlitImageInfo2-srcImageLayout-00221

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkBlitImageInfo2-srcImageLayout-01398) VUID-VkBlitImageInfo2-srcImageLayout-01398

`srcImageLayout` **must** be `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkBlitImageInfo2-srcImage-09459) VUID-VkBlitImageInfo2-srcImage-09459

If `srcImage` and `dstImage` are the same, and an elements of
`pRegions` contains the `srcSubresource` and
`dstSubresource` with matching `mipLevel` and overlapping array
layers, then the `srcImageLayout` and `dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_GENERAL`
or `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`

* 
[](#VUID-VkBlitImageInfo2-dstImage-02000) VUID-VkBlitImageInfo2-dstImage-02000

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_BLIT_DST_BIT`

* 
[](#VUID-VkBlitImageInfo2-dstImage-06422) VUID-VkBlitImageInfo2-dstImage-06422

`dstImage` **must** not use a
[format that requires a    sampler Y′CBCR conversion](formats.html#formats-requiring-sampler-ycbcr-conversion)

* 
[](#VUID-VkBlitImageInfo2-dstImage-00224) VUID-VkBlitImageInfo2-dstImage-00224

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-VkBlitImageInfo2-dstImage-00225) VUID-VkBlitImageInfo2-dstImage-00225

If `dstImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-VkBlitImageInfo2-dstImageLayout-00226) VUID-VkBlitImageInfo2-dstImageLayout-00226

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkBlitImageInfo2-dstImageLayout-01399) VUID-VkBlitImageInfo2-dstImageLayout-01399

`dstImageLayout` **must** be `VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkBlitImageInfo2-srcImage-00229) VUID-VkBlitImageInfo2-srcImage-00229

If either of `srcImage` or `dstImage` was created with a signed
integer [VkFormat](formats.html#VkFormat), the other **must** also have been created with a
signed integer [VkFormat](formats.html#VkFormat)

* 
[](#VUID-VkBlitImageInfo2-srcImage-00230) VUID-VkBlitImageInfo2-srcImage-00230

If either of `srcImage` or `dstImage` was created with an
unsigned integer [VkFormat](formats.html#VkFormat), the other **must** also have been created
with an unsigned integer [VkFormat](formats.html#VkFormat)

* 
[](#VUID-VkBlitImageInfo2-srcImage-00231) VUID-VkBlitImageInfo2-srcImage-00231

If either of `srcImage` or `dstImage` was created with a
depth/stencil format, the other **must** have exactly the same format

* 
[](#VUID-VkBlitImageInfo2-srcImage-00232) VUID-VkBlitImageInfo2-srcImage-00232

If `srcImage` was created with a depth/stencil format, `filter`
**must** be `VK_FILTER_NEAREST`

* 
[](#VUID-VkBlitImageInfo2-srcImage-00233) VUID-VkBlitImageInfo2-srcImage-00233

`srcImage` **must** have been created with a `samples` value of
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkBlitImageInfo2-dstImage-00234) VUID-VkBlitImageInfo2-dstImage-00234

`dstImage` **must** have been created with a `samples` value of
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkBlitImageInfo2-filter-02001) VUID-VkBlitImageInfo2-filter-02001

If `filter` is `VK_FILTER_LINEAR`, then the
[format features](resources.html#resources-image-format-features) of `srcImage`
**must** contain `VK_FORMAT_FEATURE_SAMPLED_IMAGE_FILTER_LINEAR_BIT`

* 
[](#VUID-VkBlitImageInfo2-filter-02002) VUID-VkBlitImageInfo2-filter-02002

If `filter` is `VK_FILTER_CUBIC_EXT`, then the
[format features](resources.html#resources-image-format-features) of `srcImage`
**must** contain `VK_FORMAT_FEATURE_SAMPLED_IMAGE_FILTER_CUBIC_BIT_EXT`

* 
[](#VUID-VkBlitImageInfo2-filter-00237) VUID-VkBlitImageInfo2-filter-00237

If `filter` is `VK_FILTER_CUBIC_EXT`, `srcImage` **must** be of
type `VK_IMAGE_TYPE_2D`

* 
[](#VUID-VkBlitImageInfo2-srcSubresource-01705) VUID-VkBlitImageInfo2-srcSubresource-01705

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkBlitImageInfo2-dstSubresource-01706) VUID-VkBlitImageInfo2-dstSubresource-01706

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkBlitImageInfo2-srcSubresource-01707) VUID-VkBlitImageInfo2-srcSubresource-01707

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkBlitImageInfo2-dstSubresource-01708) VUID-VkBlitImageInfo2-dstSubresource-01708

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkBlitImageInfo2-dstImage-02545) VUID-VkBlitImageInfo2-dstImage-02545

`dstImage` and `srcImage` **must** not have been created with
`flags` containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkBlitImageInfo2-maintenance8-10207) VUID-VkBlitImageInfo2-maintenance8-10207

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled
and `srcImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcSubresource.baseArrayLayer` **must** be
`0`, and `srcSubresource.layerCount` and
`dstSubresource.layerCount` **must** each be `1`

* 
[](#VUID-VkBlitImageInfo2-maintenance8-10208) VUID-VkBlitImageInfo2-maintenance8-10208

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled
and `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstSubresource.baseArrayLayer` **must** be
`0`, and `srcSubresource.layerCount` and
`dstSubresource.layerCount` **must** each be `1`

* 
[](#VUID-VkBlitImageInfo2-maintenance8-10579) VUID-VkBlitImageInfo2-maintenance8-10579

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled,
`dstImage` is `VK_IMAGE_TYPE_3D`, and `srcImage` is not of
type `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
the absolute difference of the `z` member of each member of
`dstOffsets` **must** equal `srcSubresource.layerCount`

* 
[](#VUID-VkBlitImageInfo2-maintenance8-10580) VUID-VkBlitImageInfo2-maintenance8-10580

If the [`maintenance8`](features.html#features-maintenance8) feature is enabled,
`srcImage` is `VK_IMAGE_TYPE_3D`, and `dstImage` is not of
type `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
the absolute difference of the `z` member of each member of
`srcOffsets` **must** equal `dstSubresource.layerCount`

* 
[](#VUID-VkBlitImageInfo2-srcImage-00240) VUID-VkBlitImageInfo2-srcImage-00240

    If
the [`maintenance8`](features.html#features-maintenance8) feature is not enabled and
    either `srcImage` or `dstImage` is of type
    `VK_IMAGE_TYPE_3D`, then for each element of `pRegions`,
    `srcSubresource.baseArrayLayer` and
    `dstSubresource.baseArrayLayer` **must** each be `0`, and
    `srcSubresource.layerCount` and `dstSubresource.layerCount`
    **must** each be `1`

* 
[](#VUID-VkBlitImageInfo2-aspectMask-00241) VUID-VkBlitImageInfo2-aspectMask-00241

For each element of `pRegions`, `srcSubresource.aspectMask`
**must** specify aspects present in `srcImage`

* 
[](#VUID-VkBlitImageInfo2-aspectMask-00242) VUID-VkBlitImageInfo2-aspectMask-00242

For each element of `pRegions`, `dstSubresource.aspectMask`
**must** specify aspects present in `dstImage`

* 
[](#VUID-VkBlitImageInfo2-srcOffset-00243) VUID-VkBlitImageInfo2-srcOffset-00243

For each element of `pRegions`, `srcOffsets`[0].x and
`srcOffsets`[1].x **must** both be greater than or equal to `0` and
less than or equal to the width of the specified `srcSubresource` of
`srcImage`

* 
[](#VUID-VkBlitImageInfo2-srcOffset-00244) VUID-VkBlitImageInfo2-srcOffset-00244

For each element of `pRegions`, `srcOffsets`[0].y and
`srcOffsets`[1].y **must** both be greater than or equal to `0` and
less than or equal to the height of the specified `srcSubresource`
of `srcImage`

* 
[](#VUID-VkBlitImageInfo2-srcImage-00245) VUID-VkBlitImageInfo2-srcImage-00245

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffsets`[0].y **must** be `0` and
`srcOffsets`[1].y **must** be `1`

* 
[](#VUID-VkBlitImageInfo2-srcOffset-00246) VUID-VkBlitImageInfo2-srcOffset-00246

For each element of `pRegions`, `srcOffsets`[0].z and
`srcOffsets`[1].z **must** both be greater than or equal to `0` and
less than or equal to the depth of the specified `srcSubresource` of
`srcImage`

* 
[](#VUID-VkBlitImageInfo2-srcImage-00247) VUID-VkBlitImageInfo2-srcImage-00247

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`srcOffsets`[0].z **must** be `0` and `srcOffsets`[1].z **must** be
`1`

* 
[](#VUID-VkBlitImageInfo2-dstOffset-00248) VUID-VkBlitImageInfo2-dstOffset-00248

For each element of `pRegions`, `dstOffsets`[0].x and
`dstOffsets`[1].x **must** both be greater than or equal to `0` and
less than or equal to the width of the specified `dstSubresource` of
`dstImage`

* 
[](#VUID-VkBlitImageInfo2-dstOffset-00249) VUID-VkBlitImageInfo2-dstOffset-00249

For each element of `pRegions`, `dstOffsets`[0].y and
`dstOffsets`[1].y **must** both be greater than or equal to `0` and
less than or equal to the height of the specified `dstSubresource`
of `dstImage`

* 
[](#VUID-VkBlitImageInfo2-dstImage-00250) VUID-VkBlitImageInfo2-dstImage-00250

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffsets`[0].y **must** be `0` and
`dstOffsets`[1].y **must** be `1`

* 
[](#VUID-VkBlitImageInfo2-dstOffset-00251) VUID-VkBlitImageInfo2-dstOffset-00251

For each element of `pRegions`, `dstOffsets`[0].z and
`dstOffsets`[1].z **must** both be greater than or equal to `0` and
less than or equal to the depth of the specified `dstSubresource` of
`dstImage`

* 
[](#VUID-VkBlitImageInfo2-dstImage-00252) VUID-VkBlitImageInfo2-dstImage-00252

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`dstOffsets`[0].z **must** be `0` and `dstOffsets`[1].z **must** be
`1`

* 
[](#VUID-VkBlitImageInfo2-pRegions-04561) VUID-VkBlitImageInfo2-pRegions-04561

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`srcImage` and `dstImage` **must** not be block-compressed images

* 
[](#VUID-VkBlitImageInfo2KHR-pRegions-06207) VUID-VkBlitImageInfo2KHR-pRegions-06207

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`srcImage` **must** be of type `VK_IMAGE_TYPE_2D`

* 
[](#VUID-VkBlitImageInfo2KHR-pRegions-06208) VUID-VkBlitImageInfo2KHR-pRegions-06208

If any element of `pRegions` contains
[VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) in its `pNext` chain, then
`srcImage` **must** not have a [multi-planar    format](formats.html#formats-multiplanar)

* 
[](#VUID-VkBlitImageInfo2-filter-09204) VUID-VkBlitImageInfo2-filter-09204

If `filter` is `VK_FILTER_CUBIC_EXT` and if the
[selectableCubicWeights](features.html#features-selectableCubicWeights) feature is
not enabled then the cubic weights **must** be
`VK_CUBIC_FILTER_WEIGHTS_CATMULL_ROM_QCOM`

Valid Usage (Implicit)

* 
[](#VUID-VkBlitImageInfo2-sType-sType) VUID-VkBlitImageInfo2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_BLIT_IMAGE_INFO_2`

* 
[](#VUID-VkBlitImageInfo2-pNext-pNext) VUID-VkBlitImageInfo2-pNext-pNext

 `pNext` **must** be `NULL` or a pointer to a valid instance of [VkBlitImageCubicWeightsInfoQCOM](#VkBlitImageCubicWeightsInfoQCOM)

* 
[](#VUID-VkBlitImageInfo2-sType-unique) VUID-VkBlitImageInfo2-sType-unique

 The `sType` value of each structure in the `pNext` chain **must** be unique

* 
[](#VUID-VkBlitImageInfo2-srcImage-parameter) VUID-VkBlitImageInfo2-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkBlitImageInfo2-srcImageLayout-parameter) VUID-VkBlitImageInfo2-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkBlitImageInfo2-dstImage-parameter) VUID-VkBlitImageInfo2-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkBlitImageInfo2-dstImageLayout-parameter) VUID-VkBlitImageInfo2-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkBlitImageInfo2-pRegions-parameter) VUID-VkBlitImageInfo2-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageBlit2](#VkImageBlit2) structures

* 
[](#VUID-VkBlitImageInfo2-filter-parameter) VUID-VkBlitImageInfo2-filter-parameter

 `filter` **must** be a valid [VkFilter](samplers.html#VkFilter) value

* 
[](#VUID-VkBlitImageInfo2-regionCount-arraylength) VUID-VkBlitImageInfo2-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkBlitImageInfo2-commonparent) VUID-VkBlitImageInfo2-commonparent

 Both of `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

If `filter` is `VK_FILTER_CUBIC_EXT` and if the `pNext` chain of
[VkBlitImageInfo2](#VkBlitImageInfo2) includes a `VkBlitImageCubicWeightsInfoQCOM`
structure, then that structure specifies cubic weights are used in the blit.
If that structure is not present, then cubic weights are considered to be
`VK_CUBIC_FILTER_WEIGHTS_CATMULL_ROM_QCOM`.

The `VkBlitImageCubicWeightsInfoQCOM` structure is defined as:

// Provided by VK_QCOM_filter_cubic_weights
typedef struct VkBlitImageCubicWeightsInfoQCOM {
    VkStructureType             sType;
    const void*                 pNext;
    VkCubicFilterWeightsQCOM    cubicWeights;
} VkBlitImageCubicWeightsInfoQCOM;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`cubicWeights` is a [VkCubicFilterWeightsQCOM](samplers.html#VkCubicFilterWeightsQCOM) value controlling
cubic filter weights for the blit.

Valid Usage (Implicit)

* 
[](#VUID-VkBlitImageCubicWeightsInfoQCOM-sType-sType) VUID-VkBlitImageCubicWeightsInfoQCOM-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_BLIT_IMAGE_CUBIC_WEIGHTS_INFO_QCOM`

* 
[](#VUID-VkBlitImageCubicWeightsInfoQCOM-cubicWeights-parameter) VUID-VkBlitImageCubicWeightsInfoQCOM-cubicWeights-parameter

 `cubicWeights` **must** be a valid [VkCubicFilterWeightsQCOM](samplers.html#VkCubicFilterWeightsQCOM) value

The `VkImageBlit2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkImageBlit2 {
    VkStructureType             sType;
    const void*                 pNext;
    VkImageSubresourceLayers    srcSubresource;
    VkOffset3D                  srcOffsets[2];
    VkImageSubresourceLayers    dstSubresource;
    VkOffset3D                  dstOffsets[2];
} VkImageBlit2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkImageBlit2 VkImageBlit2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcSubresource` is the subresource to blit from.

* 
`srcOffsets` is a pointer to an array of two [VkOffset3D](fundamentals.html#VkOffset3D)
structures specifying the bounds of the source region within
`srcSubresource`.

* 
`dstSubresource` is the subresource to blit into.

* 
`dstOffsets` is a pointer to an array of two [VkOffset3D](fundamentals.html#VkOffset3D)
structures specifying the bounds of the destination region within
`dstSubresource`.

For each element of the `pRegions` array, a blit operation is performed
for the specified source and destination regions.

Valid Usage

* 
[](#VUID-VkImageBlit2-aspectMask-00238) VUID-VkImageBlit2-aspectMask-00238

The `aspectMask` member of `srcSubresource` and
`dstSubresource` **must** match

* 
[](#VUID-VkImageBlit2-layerCount-08800) VUID-VkImageBlit2-layerCount-08800

If neither of the `layerCount` members of `srcSubresource` or
`dstSubresource` are `VK_REMAINING_ARRAY_LAYERS`, the
`layerCount` members of `srcSubresource` or `dstSubresource`
**must** match

* 
[](#VUID-VkImageBlit2-layerCount-08801) VUID-VkImageBlit2-layerCount-08801

If one of the `layerCount` members of `srcSubresource` or
`dstSubresource` is `VK_REMAINING_ARRAY_LAYERS`, the other
member **must** be either `VK_REMAINING_ARRAY_LAYERS` or equal to the
`arrayLayers` member of the [VkImageCreateInfo](resources.html#VkImageCreateInfo) used to create
the image minus `baseArrayLayer`

Valid Usage (Implicit)

* 
[](#VUID-VkImageBlit2-sType-sType) VUID-VkImageBlit2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_IMAGE_BLIT_2`

* 
[](#VUID-VkImageBlit2-pNext-pNext) VUID-VkImageBlit2-pNext-pNext

 `pNext` **must** be `NULL` or a pointer to a valid instance of [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM)

* 
[](#VUID-VkImageBlit2-sType-unique) VUID-VkImageBlit2-sType-unique

 The `sType` value of each structure in the `pNext` chain **must** be unique

* 
[](#VUID-VkImageBlit2-srcSubresource-parameter) VUID-VkImageBlit2-srcSubresource-parameter

 `srcSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

* 
[](#VUID-VkImageBlit2-dstSubresource-parameter) VUID-VkImageBlit2-dstSubresource-parameter

 `dstSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

For [vkCmdBlitImage2](#vkCmdBlitImage2), each region copied can include a rotation.
To specify a rotated region, add [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) to the
`pNext` chain of [VkImageBlit2](#VkImageBlit2).
For each region with a rotation specified,
[Image Blits with Scaling and Rotation](#copies-images-scaling-rotation)
specifies how coordinates are rotated prior to sampling from the source
image.
When rotation is specified, the source and destination images **must** each be
2D images, have a 1x1x1 [texel block extent](formats.html#formats-compatibility-classes), and only one plane.

When [VkCopyCommandTransformInfoQCOM](#VkCopyCommandTransformInfoQCOM) is in the `pNext` chain of
[VkImageBlit2](#VkImageBlit2), the specified region is rotated during the blit.
The following description of rotated addressing replaces the description in
[vkCmdBlitImage](#vkCmdBlitImage).

The following code computes rotation of normalized coordinates.

// rotation of normalized coordinates
VkOffset2D RotateNormUV(VkOffset2D in, VkSurfaceTransformFlagBitsKHR flags)
{
    VkOffset2D output;
    switch (flags)
    {
        case VK_SURFACE_TRANSFORM_IDENTITY_BIT_KHR:
            out.x = in.x;
            out.y = in.y;
            break;
        case VK_SURFACE_TRANSFORM_ROTATE_90_BIT_KHR:
            out.x = in.y;
            out.y = 1.0 - in.x;
            break;
        case VK_SURFACE_TRANSFORM_ROTATE_180_BIT_KHR:
            out.x = 1.0 - in.x;
            out.y = 1.0 - in.y;
            break;
        case VK_SURFACE_TRANSFORM_ROTATE_270_BIT_KHR:
            out.x = 1.0 - in.y;
            out.y = in.x;
            break;
    }
    return out;
}

* 
For each destination texel, the integer coordinate of that texel is
converted to an unnormalized texture coordinate, using the effective
inverse of the equations described in
[unnormalized to integer    conversion](textures.html#textures-unnormalized-to-integer):

ubase = i +  ½

vbase = j +  ½

wbase = k +  ½

* 
These base coordinates are then offset by the first destination offset:

uoffset = ubase - xdst0

voffset = vbase - ydst0

woffset = wbase - zdst0

aoffset = a - `baseArrayCount`dst

* 
The UV destination coordinates are scaled by the destination region,
rotated, and scaled by the source region.

udest_scaled = uoffset / (xdst1 - xdst0)

vdest_scaled = voffset / (ydst1 - ydst0)

(usrc_scaled, vsrc_scaled) =
`RotateNormUV`(udest_scaled, vdest_scaled,
`transform`)

uscaled = usrc_scaled × (xSrc1 - xSrc0)

vscaled = vsrc_scaled × (ySrc1 - ySrc0)

* 
The W coordinate is unaffected by rotation.
The scale is determined from the ratio of source and destination
regions, and applied to the offset coordinate:

scalew = (zSrc1 - zSrc0) / (zdst1 - zdst0)

wscaled = woffset × scalew

* 
Finally the source offset is added to the scaled source coordinates, to
determine the final unnormalized coordinates used to sample from
`srcImage`:

u = uscaled +  xSrc0

v = vscaled +  ySrc0

w = wscaled +  zSrc0

q = `mipLevel`

a = aoffset +  `baseArrayCount`src

These coordinates are used to sample from the source image as described for
[Image Operations](textures.html#textures), with the filter mode equal to that of
`filter`; a mipmap mode of `VK_SAMPLER_MIPMAP_MODE_NEAREST`; and an
address mode of `VK_SAMPLER_ADDRESS_MODE_CLAMP_TO_EDGE`.
Implementations **must** clamp at the edge of the source image, and **may**
additionally clamp to the edge of the source region.

To resolve a multisample color image to a non-multisample color image, call:

// Provided by VK_VERSION_1_0
void vkCmdResolveImage(
    VkCommandBuffer                             commandBuffer,
    VkImage                                     srcImage,
    VkImageLayout                               srcImageLayout,
    VkImage                                     dstImage,
    VkImageLayout                               dstImageLayout,
    uint32_t                                    regionCount,
    const VkImageResolve*                       pRegions);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the resolve.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the resolve.

* 
`regionCount` is the number of regions to resolve.

* 
`pRegions` is a pointer to an array of [VkImageResolve](#VkImageResolve)
structures specifying the regions to resolve.

During the resolve the samples corresponding to each pixel location in the
source are converted to a single sample before being written to the
destination.

If the source format is a floating-point or normalized type, the resolve
mode is chosen as implementation-dependent behavior.
If the resolve mode requires to calculate the result from multiple samples,
such as by computing an average or weighted average of the samples, the
values for each pixel are resolved with implementation-defined numerical
precision.

If the [numeric format](formats.html#formats-numericformat) of `srcImage` uses sRGB
encoding and the resolve mode requires the implementation to convert the
samples to floating-point to perform the calculations, the implementation
**should** convert samples from nonlinear to linear before resolving the
samples as described in the “sRGB EOTF” section of the
[Khronos Data Format Specification](introduction.html#data-format).
In this case, the implementation **must** convert the linear averaged value to
nonlinear before writing the resolved result to `dstImage`.

If the source format is an integer type, a single sample’s value is selected
for each pixel.

`srcOffset` and `dstOffset` select the initial `x`, `y`, and
`z` offsets in texels of the sub-regions of the source and destination
image data.
`extent` is the size in texels of the source image to resolve in
`width`, `height` and `depth`.
Each element of `pRegions` **must** be a region that is contained within
its corresponding image.

Resolves are done layer by layer starting with `baseArrayLayer` member
of `srcSubresource` for the source and `dstSubresource` for the
destination.
`layerCount` layers are resolved to the destination image.

Valid Usage

* 
[](#VUID-vkCmdResolveImage-commandBuffer-01837) VUID-vkCmdResolveImage-commandBuffer-01837

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdResolveImage-commandBuffer-01838) VUID-vkCmdResolveImage-commandBuffer-01838

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdResolveImage-commandBuffer-01839) VUID-vkCmdResolveImage-commandBuffer-01839

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

* 
[](#VUID-vkCmdResolveImage-pRegions-00255) VUID-vkCmdResolveImage-pRegions-00255

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-vkCmdResolveImage-srcImage-00256) VUID-vkCmdResolveImage-srcImage-00256

If `srcImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdResolveImage-srcImage-00257) VUID-vkCmdResolveImage-srcImage-00257

`srcImage` **must** have a sample count equal to any valid sample count
value other than `VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-vkCmdResolveImage-dstImage-00258) VUID-vkCmdResolveImage-dstImage-00258

If `dstImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdResolveImage-dstImage-00259) VUID-vkCmdResolveImage-dstImage-00259

`dstImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-vkCmdResolveImage-srcImageLayout-00260) VUID-vkCmdResolveImage-srcImageLayout-00260

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdResolveImage-srcImageLayout-01400) VUID-vkCmdResolveImage-srcImageLayout-01400

`srcImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdResolveImage-dstImageLayout-00262) VUID-vkCmdResolveImage-dstImageLayout-00262

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-vkCmdResolveImage-dstImageLayout-01401) VUID-vkCmdResolveImage-dstImageLayout-01401

`dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-vkCmdResolveImage-dstImage-02003) VUID-vkCmdResolveImage-dstImage-02003

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain
`VK_FORMAT_FEATURE_COLOR_ATTACHMENT_BIT`

* 
[](#VUID-vkCmdResolveImage-linearColorAttachment-06519) VUID-vkCmdResolveImage-linearColorAttachment-06519

If the [`linearColorAttachment`](features.html#features-linearColorAttachment)
feature is enabled and the image is created with
`VK_IMAGE_TILING_LINEAR`, the
[format features](resources.html#resources-image-format-features) of `dstImage`
**must** contain `VK_FORMAT_FEATURE_2_LINEAR_COLOR_ATTACHMENT_BIT_NV`

* 
[](#VUID-vkCmdResolveImage-srcImage-01386) VUID-vkCmdResolveImage-srcImage-01386

`srcImage` and `dstImage` **must** have been created with the same
image format

* 
[](#VUID-vkCmdResolveImage-srcSubresource-01709) VUID-vkCmdResolveImage-srcSubresource-01709

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdResolveImage-dstSubresource-01710) VUID-vkCmdResolveImage-dstSubresource-01710

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdResolveImage-srcSubresource-01711) VUID-vkCmdResolveImage-srcSubresource-01711

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-vkCmdResolveImage-dstSubresource-01712) VUID-vkCmdResolveImage-dstSubresource-01712

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-vkCmdResolveImage-dstImage-02546) VUID-vkCmdResolveImage-dstImage-02546

`dstImage` and `srcImage` **must** not have been created with
`flags` containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-vkCmdResolveImage-srcImage-04446) VUID-vkCmdResolveImage-srcImage-04446

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcSubresource.layerCount` **must** be `1`

* 
[](#VUID-vkCmdResolveImage-srcImage-04447) VUID-vkCmdResolveImage-srcImage-04447

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstSubresource.baseArrayLayer` **must** be
`0` and `dstSubresource.layerCount` **must** be `1`

* 
[](#VUID-vkCmdResolveImage-srcOffset-00269) VUID-vkCmdResolveImage-srcOffset-00269

For each element of `pRegions`, `srcOffset.x` and
(`extent.width` +  `srcOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-vkCmdResolveImage-srcOffset-00270) VUID-vkCmdResolveImage-srcOffset-00270

For each element of `pRegions`, `srcOffset.y` and
(`extent.height` +  `srcOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-vkCmdResolveImage-srcImage-00271) VUID-vkCmdResolveImage-srcImage-00271

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-vkCmdResolveImage-srcOffset-00272) VUID-vkCmdResolveImage-srcOffset-00272

For each element of `pRegions`, `srcOffset.z` and
(`extent.depth` +  `srcOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-vkCmdResolveImage-srcImage-00273) VUID-vkCmdResolveImage-srcImage-00273

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`srcOffset.z` **must** be `0` and `extent.depth` **must** be `1`

* 
[](#VUID-vkCmdResolveImage-dstOffset-00274) VUID-vkCmdResolveImage-dstOffset-00274

For each element of `pRegions`, `dstOffset.x` and
(`extent.width` +  `dstOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-vkCmdResolveImage-dstOffset-00275) VUID-vkCmdResolveImage-dstOffset-00275

For each element of `pRegions`, `dstOffset.y` and
(`extent.height` +  `dstOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-vkCmdResolveImage-dstImage-00276) VUID-vkCmdResolveImage-dstImage-00276

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-vkCmdResolveImage-dstOffset-00277) VUID-vkCmdResolveImage-dstOffset-00277

For each element of `pRegions`, `dstOffset.z` and
(`extent.depth` +  `dstOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-vkCmdResolveImage-dstImage-00278) VUID-vkCmdResolveImage-dstImage-00278

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`dstOffset.z` **must** be `0` and `extent.depth` **must** be `1`

* 
[](#VUID-vkCmdResolveImage-srcImage-06762) VUID-vkCmdResolveImage-srcImage-06762

`srcImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-vkCmdResolveImage-srcImage-06763) VUID-vkCmdResolveImage-srcImage-06763

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_SRC_BIT`

* 
[](#VUID-vkCmdResolveImage-dstImage-06764) VUID-vkCmdResolveImage-dstImage-06764

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdResolveImage-dstImage-06765) VUID-vkCmdResolveImage-dstImage-06765

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_DST_BIT`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdResolveImage-commandBuffer-parameter) VUID-vkCmdResolveImage-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdResolveImage-srcImage-parameter) VUID-vkCmdResolveImage-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdResolveImage-srcImageLayout-parameter) VUID-vkCmdResolveImage-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdResolveImage-dstImage-parameter) VUID-vkCmdResolveImage-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-vkCmdResolveImage-dstImageLayout-parameter) VUID-vkCmdResolveImage-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-vkCmdResolveImage-pRegions-parameter) VUID-vkCmdResolveImage-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageResolve](#VkImageResolve) structures

* 
[](#VUID-vkCmdResolveImage-commandBuffer-recording) VUID-vkCmdResolveImage-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdResolveImage-commandBuffer-cmdpool) VUID-vkCmdResolveImage-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics operations

* 
[](#VUID-vkCmdResolveImage-renderpass) VUID-vkCmdResolveImage-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdResolveImage-videocoding) VUID-vkCmdResolveImage-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdResolveImage-regionCount-arraylength) VUID-vkCmdResolveImage-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-vkCmdResolveImage-commonparent) VUID-vkCmdResolveImage-commonparent

 Each of `commandBuffer`, `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Graphics
Action

The `VkImageResolve` structure is defined as:

// Provided by VK_VERSION_1_0
typedef struct VkImageResolve {
    VkImageSubresourceLayers    srcSubresource;
    VkOffset3D                  srcOffset;
    VkImageSubresourceLayers    dstSubresource;
    VkOffset3D                  dstOffset;
    VkExtent3D                  extent;
} VkImageResolve;

* 
`srcSubresource` and `dstSubresource` are
[VkImageSubresourceLayers](#VkImageSubresourceLayers) structures specifying the image
subresources of the images used for the source and destination image
data, respectively.
Resolve of depth/stencil images is not supported.

* 
`srcOffset` and `dstOffset` select the initial `x`, `y`,
and `z` offsets in texels of the sub-regions of the source and
destination image data.

* 
`extent` is the size in texels of the source image to resolve in
`width`, `height` and `depth`.

Valid Usage

* 
[](#VUID-VkImageResolve-aspectMask-00266) VUID-VkImageResolve-aspectMask-00266

The `aspectMask` member of `srcSubresource` and
`dstSubresource` **must** only contain `VK_IMAGE_ASPECT_COLOR_BIT`

* 
[](#VUID-VkImageResolve-layerCount-08803) VUID-VkImageResolve-layerCount-08803

If neither of the `layerCount` members of `srcSubresource` or
`dstSubresource` are `VK_REMAINING_ARRAY_LAYERS`, the
`layerCount` member of `srcSubresource` and `dstSubresource`
**must** match

* 
[](#VUID-VkImageResolve-layerCount-08804) VUID-VkImageResolve-layerCount-08804

If one of the `layerCount` members of `srcSubresource` or
`dstSubresource` is `VK_REMAINING_ARRAY_LAYERS`, the other
member **must** be either `VK_REMAINING_ARRAY_LAYERS` or equal to the
`arrayLayers` member of the [VkImageCreateInfo](resources.html#VkImageCreateInfo) used to create
the image minus `baseArrayLayer`

Valid Usage (Implicit)

* 
[](#VUID-VkImageResolve-srcSubresource-parameter) VUID-VkImageResolve-srcSubresource-parameter

 `srcSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

* 
[](#VUID-VkImageResolve-dstSubresource-parameter) VUID-VkImageResolve-dstSubresource-parameter

 `dstSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

A more extensible version of the resolve image command is defined below.

To resolve a multisample image to a non-multisample image, call:

// Provided by VK_VERSION_1_3
void vkCmdResolveImage2(
    VkCommandBuffer                             commandBuffer,
    const VkResolveImageInfo2*                  pResolveImageInfo);

or the equivalent command

// Provided by VK_KHR_copy_commands2
void vkCmdResolveImage2KHR(
    VkCommandBuffer                             commandBuffer,
    const VkResolveImageInfo2*                  pResolveImageInfo);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`pResolveImageInfo` is a pointer to a [VkResolveImageInfo2](#VkResolveImageInfo2)
structure describing the resolve parameters.

This command is functionally identical to [vkCmdResolveImage](#vkCmdResolveImage), but
includes extensible sub-structures that include `sType` and `pNext`
parameters, allowing them to be more easily extended.

Valid Usage

* 
[](#VUID-vkCmdResolveImage2-commandBuffer-01837) VUID-vkCmdResolveImage2-commandBuffer-01837

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`srcImage` **must** not be a protected image

* 
[](#VUID-vkCmdResolveImage2-commandBuffer-01838) VUID-vkCmdResolveImage2-commandBuffer-01838

If `commandBuffer` is an unprotected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be a protected image

* 
[](#VUID-vkCmdResolveImage2-commandBuffer-01839) VUID-vkCmdResolveImage2-commandBuffer-01839

If `commandBuffer` is a protected command buffer and
[`protectedNoFault`](devsandqueues.html#limits-protectedNoFault) is not supported,
`dstImage` **must** not be an unprotected image

Valid Usage (Implicit)

* 
[](#VUID-vkCmdResolveImage2-commandBuffer-parameter) VUID-vkCmdResolveImage2-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdResolveImage2-pResolveImageInfo-parameter) VUID-vkCmdResolveImage2-pResolveImageInfo-parameter

 `pResolveImageInfo` **must** be a valid pointer to a valid [VkResolveImageInfo2](#VkResolveImageInfo2) structure

* 
[](#VUID-vkCmdResolveImage2-commandBuffer-recording) VUID-vkCmdResolveImage2-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdResolveImage2-commandBuffer-cmdpool) VUID-vkCmdResolveImage2-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics operations

* 
[](#VUID-vkCmdResolveImage2-renderpass) VUID-vkCmdResolveImage2-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdResolveImage2-videocoding) VUID-vkCmdResolveImage2-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Graphics
Action

The `VkResolveImageInfo2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkResolveImageInfo2 {
    VkStructureType           sType;
    const void*               pNext;
    VkImage                   srcImage;
    VkImageLayout             srcImageLayout;
    VkImage                   dstImage;
    VkImageLayout             dstImageLayout;
    uint32_t                  regionCount;
    const VkImageResolve2*    pRegions;
} VkResolveImageInfo2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkResolveImageInfo2 VkResolveImageInfo2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcImage` is the source image.

* 
`srcImageLayout` is the layout of the source image subresources for
the resolve.

* 
`dstImage` is the destination image.

* 
`dstImageLayout` is the layout of the destination image subresources
for the resolve.

* 
`regionCount` is the number of regions to resolve.

* 
`pRegions` is a pointer to an array of [VkImageResolve2](#VkImageResolve2)
structures specifying the regions to resolve.

Valid Usage

* 
[](#VUID-VkResolveImageInfo2-pRegions-00255) VUID-VkResolveImageInfo2-pRegions-00255

The union of all source regions, and the union of all destination
regions, specified by the elements of `pRegions`, **must** not overlap
in memory

* 
[](#VUID-VkResolveImageInfo2-srcImage-00256) VUID-VkResolveImageInfo2-srcImage-00256

If `srcImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-VkResolveImageInfo2-srcImage-00257) VUID-VkResolveImageInfo2-srcImage-00257

`srcImage` **must** have a sample count equal to any valid sample count
value other than `VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkResolveImageInfo2-dstImage-00258) VUID-VkResolveImageInfo2-dstImage-00258

If `dstImage` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-VkResolveImageInfo2-dstImage-00259) VUID-VkResolveImageInfo2-dstImage-00259

`dstImage` **must** have a sample count equal to
`VK_SAMPLE_COUNT_1_BIT`

* 
[](#VUID-VkResolveImageInfo2-srcImageLayout-00260) VUID-VkResolveImageInfo2-srcImageLayout-00260

`srcImageLayout` **must** specify the layout of the image subresources
of `srcImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkResolveImageInfo2-srcImageLayout-01400) VUID-VkResolveImageInfo2-srcImageLayout-01400

`srcImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_SRC_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkResolveImageInfo2-dstImageLayout-00262) VUID-VkResolveImageInfo2-dstImageLayout-00262

`dstImageLayout` **must** specify the layout of the image subresources
of `dstImage` specified in `pRegions` at the time this command
is executed on a `VkDevice`

* 
[](#VUID-VkResolveImageInfo2-dstImageLayout-01401) VUID-VkResolveImageInfo2-dstImageLayout-01401

`dstImageLayout` **must** be
`VK_IMAGE_LAYOUT_SHARED_PRESENT_KHR`,
`VK_IMAGE_LAYOUT_TRANSFER_DST_OPTIMAL` or
`VK_IMAGE_LAYOUT_GENERAL`

* 
[](#VUID-VkResolveImageInfo2-dstImage-02003) VUID-VkResolveImageInfo2-dstImage-02003

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain
`VK_FORMAT_FEATURE_COLOR_ATTACHMENT_BIT`

* 
[](#VUID-VkResolveImageInfo2-linearColorAttachment-06519) VUID-VkResolveImageInfo2-linearColorAttachment-06519

If the [`linearColorAttachment`](features.html#features-linearColorAttachment)
feature is enabled and the image is created with
`VK_IMAGE_TILING_LINEAR`, the
[format features](resources.html#resources-image-format-features) of `dstImage`
**must** contain `VK_FORMAT_FEATURE_2_LINEAR_COLOR_ATTACHMENT_BIT_NV`

* 
[](#VUID-VkResolveImageInfo2-srcImage-01386) VUID-VkResolveImageInfo2-srcImage-01386

`srcImage` and `dstImage` **must** have been created with the same
image format

* 
[](#VUID-VkResolveImageInfo2-srcSubresource-01709) VUID-VkResolveImageInfo2-srcSubresource-01709

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkResolveImageInfo2-dstSubresource-01710) VUID-VkResolveImageInfo2-dstSubresource-01710

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkResolveImageInfo2-srcSubresource-01711) VUID-VkResolveImageInfo2-srcSubresource-01711

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `srcImage` was created

* 
[](#VUID-VkResolveImageInfo2-dstSubresource-01712) VUID-VkResolveImageInfo2-dstSubresource-01712

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](resources.html#VkImageCreateInfo) when `dstImage` was created

* 
[](#VUID-VkResolveImageInfo2-dstImage-02546) VUID-VkResolveImageInfo2-dstImage-02546

`dstImage` and `srcImage` **must** not have been created with
`flags` containing `VK_IMAGE_CREATE_SUBSAMPLED_BIT_EXT`

* 
[](#VUID-VkResolveImageInfo2-srcImage-04446) VUID-VkResolveImageInfo2-srcImage-04446

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `srcSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkResolveImageInfo2-srcImage-04447) VUID-VkResolveImageInfo2-srcImage-04447

If `dstImage` is of type `VK_IMAGE_TYPE_3D`, then for each
element of `pRegions`, `dstSubresource.baseArrayLayer` **must** be
`0` and `dstSubresource.layerCount` **must** be `1`

* 
[](#VUID-VkResolveImageInfo2-srcOffset-00269) VUID-VkResolveImageInfo2-srcOffset-00269

For each element of `pRegions`, `srcOffset.x` and
(`extent.width` +  `srcOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkResolveImageInfo2-srcOffset-00270) VUID-VkResolveImageInfo2-srcOffset-00270

For each element of `pRegions`, `srcOffset.y` and
(`extent.height` +  `srcOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkResolveImageInfo2-srcImage-00271) VUID-VkResolveImageInfo2-srcImage-00271

If `srcImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `srcOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-VkResolveImageInfo2-srcOffset-00272) VUID-VkResolveImageInfo2-srcOffset-00272

For each element of `pRegions`, `srcOffset.z` and
(`extent.depth` +  `srcOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `srcSubresource` of `srcImage`

* 
[](#VUID-VkResolveImageInfo2-srcImage-00273) VUID-VkResolveImageInfo2-srcImage-00273

If `srcImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`srcOffset.z` **must** be `0` and `extent.depth` **must** be `1`

* 
[](#VUID-VkResolveImageInfo2-dstOffset-00274) VUID-VkResolveImageInfo2-dstOffset-00274

For each element of `pRegions`, `dstOffset.x` and
(`extent.width` +  `dstOffset.x`) **must** both be
greater than or equal to `0` and less than or equal to the width of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkResolveImageInfo2-dstOffset-00275) VUID-VkResolveImageInfo2-dstOffset-00275

For each element of `pRegions`, `dstOffset.y` and
(`extent.height` +  `dstOffset.y`) **must** both be
greater than or equal to `0` and less than or equal to the height of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkResolveImageInfo2-dstImage-00276) VUID-VkResolveImageInfo2-dstImage-00276

If `dstImage` is of type `VK_IMAGE_TYPE_1D`, then for each
element of `pRegions`, `dstOffset.y` **must** be `0` and
`extent.height` **must** be `1`

* 
[](#VUID-VkResolveImageInfo2-dstOffset-00277) VUID-VkResolveImageInfo2-dstOffset-00277

For each element of `pRegions`, `dstOffset.z` and
(`extent.depth` +  `dstOffset.z`) **must** both be
greater than or equal to `0` and less than or equal to the depth of the
specified `dstSubresource` of `dstImage`

* 
[](#VUID-VkResolveImageInfo2-dstImage-00278) VUID-VkResolveImageInfo2-dstImage-00278

If `dstImage` is of type `VK_IMAGE_TYPE_1D` or
`VK_IMAGE_TYPE_2D`, then for each element of `pRegions`,
`dstOffset.z` **must** be `0` and `extent.depth` **must** be `1`

* 
[](#VUID-VkResolveImageInfo2-srcImage-06762) VUID-VkResolveImageInfo2-srcImage-06762

`srcImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_SRC_BIT` usage flag

* 
[](#VUID-VkResolveImageInfo2-srcImage-06763) VUID-VkResolveImageInfo2-srcImage-06763

The [format features](resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_SRC_BIT`

* 
[](#VUID-VkResolveImageInfo2-dstImage-06764) VUID-VkResolveImageInfo2-dstImage-06764

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-VkResolveImageInfo2-dstImage-06765) VUID-VkResolveImageInfo2-dstImage-06765

The [format features](resources.html#resources-image-format-features) of
`dstImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_DST_BIT`

Valid Usage (Implicit)

* 
[](#VUID-VkResolveImageInfo2-sType-sType) VUID-VkResolveImageInfo2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_RESOLVE_IMAGE_INFO_2`

* 
[](#VUID-VkResolveImageInfo2-pNext-pNext) VUID-VkResolveImageInfo2-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkResolveImageInfo2-srcImage-parameter) VUID-VkResolveImageInfo2-srcImage-parameter

 `srcImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkResolveImageInfo2-srcImageLayout-parameter) VUID-VkResolveImageInfo2-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkResolveImageInfo2-dstImage-parameter) VUID-VkResolveImageInfo2-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](resources.html#VkImage) handle

* 
[](#VUID-VkResolveImageInfo2-dstImageLayout-parameter) VUID-VkResolveImageInfo2-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](resources.html#VkImageLayout) value

* 
[](#VUID-VkResolveImageInfo2-pRegions-parameter) VUID-VkResolveImageInfo2-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageResolve2](#VkImageResolve2) structures

* 
[](#VUID-VkResolveImageInfo2-regionCount-arraylength) VUID-VkResolveImageInfo2-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkResolveImageInfo2-commonparent) VUID-VkResolveImageInfo2-commonparent

 Both of `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

The `VkImageResolve2` structure is defined as:

// Provided by VK_VERSION_1_3
typedef struct VkImageResolve2 {
    VkStructureType             sType;
    const void*                 pNext;
    VkImageSubresourceLayers    srcSubresource;
    VkOffset3D                  srcOffset;
    VkImageSubresourceLayers    dstSubresource;
    VkOffset3D                  dstOffset;
    VkExtent3D                  extent;
} VkImageResolve2;

or the equivalent

// Provided by VK_KHR_copy_commands2
typedef VkImageResolve2 VkImageResolve2KHR;

* 
`sType` is a [VkStructureType](fundamentals.html#VkStructureType) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`srcSubresource` and `dstSubresource` are
[VkImageSubresourceLayers](#VkImageSubresourceLayers) structures specifying the image
subresources of the images used for the source and destination image
data, respectively.
Resolve of depth/stencil images is not supported.

* 
`srcOffset` and `dstOffset` select the initial `x`, `y`,
and `z` offsets in texels of the sub-regions of the source and
destination image data.

* 
`extent` is the size in texels of the source image to resolve in
`width`, `height` and `depth`.

Valid Usage

* 
[](#VUID-VkImageResolve2-aspectMask-00266) VUID-VkImageResolve2-aspectMask-00266

The `aspectMask` member of `srcSubresource` and
`dstSubresource` **must** only contain `VK_IMAGE_ASPECT_COLOR_BIT`

* 
[](#VUID-VkImageResolve2-layerCount-08803) VUID-VkImageResolve2-layerCount-08803

If neither of the `layerCount` members of `srcSubresource` or
`dstSubresource` are `VK_REMAINING_ARRAY_LAYERS`, the
`layerCount` member of `srcSubresource` and `dstSubresource`
**must** match

* 
[](#VUID-VkImageResolve2-layerCount-08804) VUID-VkImageResolve2-layerCount-08804

If one of the `layerCount` members of `srcSubresource` or
`dstSubresource` is `VK_REMAINING_ARRAY_LAYERS`, the other
member **must** be either `VK_REMAINING_ARRAY_LAYERS` or equal to the
`arrayLayers` member of the [VkImageCreateInfo](resources.html#VkImageCreateInfo) used to create
the image minus `baseArrayLayer`

Valid Usage (Implicit)

* 
[](#VUID-VkImageResolve2-sType-sType) VUID-VkImageResolve2-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_IMAGE_RESOLVE_2`

* 
[](#VUID-VkImageResolve2-pNext-pNext) VUID-VkImageResolve2-pNext-pNext

 `pNext` **must** be `NULL`

* 
[](#VUID-VkImageResolve2-srcSubresource-parameter) VUID-VkImageResolve2-srcSubresource-parameter

 `srcSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

* 
[](#VUID-VkImageResolve2-dstSubresource-parameter) VUID-VkImageResolve2-dstSubresource-parameter

 `dstSubresource` **must** be a valid [VkImageSubresourceLayers](#VkImageSubresourceLayers) structure

To write a 32-bit marker value into a buffer as a pipelined operation, call:

// Provided by VK_AMD_buffer_marker with VK_VERSION_1_3 or VK_KHR_synchronization2
void vkCmdWriteBufferMarker2AMD(
    VkCommandBuffer                             commandBuffer,
    VkPipelineStageFlags2                       stage,
    VkBuffer                                    dstBuffer,
    VkDeviceSize                                dstOffset,
    uint32_t                                    marker);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`stage` specifies the pipeline stage whose completion triggers the
marker write.

* 
`dstBuffer` is the buffer where the marker will be written.

* 
`dstOffset` is the byte offset into the buffer where the marker will
be written.

* 
`marker` is the 32-bit value of the marker.

The command will write the 32-bit marker value into the buffer only after
all preceding commands have finished executing up to at least the specified
pipeline stage.
This includes the completion of other preceding
`vkCmdWriteBufferMarker2AMD` commands so long as their specified
pipeline stages occur either at the same time or earlier than this command’s
specified `stage`.

While consecutive buffer marker writes with the same `stage` parameter
implicitly complete in submission order, memory and execution dependencies
between buffer marker writes and other operations **must** still be explicitly
ordered using synchronization commands.
The access scope for buffer marker writes falls under the
`VK_ACCESS_TRANSFER_WRITE_BIT`, and the pipeline stages for identifying
the synchronization scope **must** include both `stage` and
`VK_PIPELINE_STAGE_TRANSFER_BIT`.

Valid Usage

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03929) VUID-vkCmdWriteBufferMarker2AMD-stage-03929

If the [`geometryShader`](features.html#features-geometryShader) feature is not
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_GEOMETRY_SHADER_BIT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03930) VUID-vkCmdWriteBufferMarker2AMD-stage-03930

If the [`tessellationShader`](features.html#features-tessellationShader) feature
is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_TESSELLATION_CONTROL_SHADER_BIT` or
`VK_PIPELINE_STAGE_2_TESSELLATION_EVALUATION_SHADER_BIT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03931) VUID-vkCmdWriteBufferMarker2AMD-stage-03931

If the [`conditionalRendering`](features.html#features-conditionalRendering)
feature is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_CONDITIONAL_RENDERING_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03932) VUID-vkCmdWriteBufferMarker2AMD-stage-03932

If the [`fragmentDensityMap`](features.html#features-fragmentDensityMap) feature
is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_FRAGMENT_DENSITY_PROCESS_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03933) VUID-vkCmdWriteBufferMarker2AMD-stage-03933

If the [`transformFeedback`](features.html#features-transformFeedback) feature
is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_TRANSFORM_FEEDBACK_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03934) VUID-vkCmdWriteBufferMarker2AMD-stage-03934

If the [`meshShader`](features.html#features-meshShader) feature is not enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_MESH_SHADER_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03935) VUID-vkCmdWriteBufferMarker2AMD-stage-03935

If the [`taskShader`](features.html#features-taskShader) feature is not enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_TASK_SHADER_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-07316) VUID-vkCmdWriteBufferMarker2AMD-stage-07316

If neither of the [`shadingRateImage`](features.html#features-shadingRateImage)
or the [    `attachmentFragmentShadingRate`](features.html#features-attachmentFragmentShadingRate) features are enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_FRAGMENT_SHADING_RATE_ATTACHMENT_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-04957) VUID-vkCmdWriteBufferMarker2AMD-stage-04957

If the [`subpassShading`](features.html#features-subpassShading) feature is not
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_SUBPASS_SHADER_BIT_HUAWEI`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-04995) VUID-vkCmdWriteBufferMarker2AMD-stage-04995

If the [`invocationMask`](features.html#features-invocationMask) feature is not
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_INVOCATION_MASK_BIT_HUAWEI`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-07946) VUID-vkCmdWriteBufferMarker2AMD-stage-07946

If neither the [VK_NV_ray_tracing](../appendices/extensions.html#VK_NV_ray_tracing) extension or the
[`rayTracingPipeline`](features.html#features-rayTracingPipeline) feature are
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_RAY_TRACING_SHADER_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-10751) VUID-vkCmdWriteBufferMarker2AMD-stage-10751

If the [`accelerationStructure`](features.html#features-accelerationStructure)
feature is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_ACCELERATION_STRUCTURE_BUILD_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-10752) VUID-vkCmdWriteBufferMarker2AMD-stage-10752

If the [`rayTracingMaintenance1`](features.html#features-rayTracingMaintenance1)
feature is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_ACCELERATION_STRUCTURE_COPY_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-10753) VUID-vkCmdWriteBufferMarker2AMD-stage-10753

If the [`micromap`](features.html#features-micromap) feature is not enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_MICROMAP_BUILD_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-synchronization2-03893) VUID-vkCmdWriteBufferMarker2AMD-synchronization2-03893

The [`synchronization2`](features.html#features-synchronization2) feature **must**
be enabled

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03894) VUID-vkCmdWriteBufferMarker2AMD-stage-03894

`stage` **must** include only a single pipeline stage

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03895) VUID-vkCmdWriteBufferMarker2AMD-stage-03895

`stage` **must** include only stages that are valid for the queue
family that was used to create the command pool that `commandBuffer`
was allocated from

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-dstOffset-03896) VUID-vkCmdWriteBufferMarker2AMD-dstOffset-03896

`dstOffset` **must** be less than or equal to the size of
`dstBuffer` minus `4`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-03897) VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-03897

`dstBuffer` **must** have been created with the
`VK_BUFFER_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-03898) VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-03898

If `dstBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-dstOffset-03899) VUID-vkCmdWriteBufferMarker2AMD-dstOffset-03899

`dstOffset` **must** be a multiple of `4`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-parameter) VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-parameter) VUID-vkCmdWriteBufferMarker2AMD-stage-parameter

 `stage` **must** be a valid combination of [VkPipelineStageFlagBits2](synchronization.html#VkPipelineStageFlagBits2) values

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-parameter) VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-parameter

 `dstBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-recording) VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-cmdpool) VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-videocoding) VUID-vkCmdWriteBufferMarker2AMD-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-commonparent) VUID-vkCmdWriteBufferMarker2AMD-commonparent

 Both of `commandBuffer`, and `dstBuffer` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Both
Outside
Transfer

Graphics

Compute
Action

To write a 32-bit marker value into a buffer as a pipelined operation, call:

// Provided by VK_AMD_buffer_marker
void vkCmdWriteBufferMarkerAMD(
    VkCommandBuffer                             commandBuffer,
    VkPipelineStageFlagBits                     pipelineStage,
    VkBuffer                                    dstBuffer,
    VkDeviceSize                                dstOffset,
    uint32_t                                    marker);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`pipelineStage` is a [VkPipelineStageFlagBits](synchronization.html#VkPipelineStageFlagBits) value specifying
the pipeline stage whose completion triggers the marker write.

* 
`dstBuffer` is the buffer where the marker will be written to.

* 
`dstOffset` is the byte offset into the buffer where the marker will
be written to.

* 
`marker` is the 32-bit value of the marker.

The command will write the 32-bit marker value into the buffer only after
all preceding commands have finished executing up to at least the specified
pipeline stage.
This includes the completion of other preceding
`vkCmdWriteBufferMarkerAMD` commands so long as their specified pipeline
stages occur either at the same time or earlier than this command’s
specified `pipelineStage`.

While consecutive buffer marker writes with the same `pipelineStage`
parameter are implicitly complete in submission order, memory and execution
dependencies between buffer marker writes and other operations **must** still
be explicitly ordered using synchronization commands.
The access scope for buffer marker writes falls under the
`VK_ACCESS_TRANSFER_WRITE_BIT`, and the pipeline stages for identifying
the synchronization scope **must** include both `pipelineStage` and
`VK_PIPELINE_STAGE_TRANSFER_BIT`.

Valid Usage

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04074) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04074

`pipelineStage` **must** be a
[valid stage](synchronization.html#synchronization-pipeline-stages-supported) for the queue
family that was used to create the command pool that `commandBuffer`
was allocated from

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04075) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04075

If the [`geometryShader`](features.html#features-geometryShader) feature is not
enabled, `pipelineStage` **must** not be
`VK_PIPELINE_STAGE_GEOMETRY_SHADER_BIT`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04076) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04076

If the [`tessellationShader`](features.html#features-tessellationShader) feature
is not enabled, `pipelineStage` **must** not be
`VK_PIPELINE_STAGE_TESSELLATION_CONTROL_SHADER_BIT` or
`VK_PIPELINE_STAGE_TESSELLATION_EVALUATION_SHADER_BIT`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04077) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04077

If the [`conditionalRendering`](features.html#features-conditionalRendering)
feature is not enabled, `pipelineStage` **must** not be
`VK_PIPELINE_STAGE_CONDITIONAL_RENDERING_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04078) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04078

If the [`fragmentDensityMap`](features.html#features-fragmentDensityMap) feature
is not enabled, `pipelineStage` **must** not be
`VK_PIPELINE_STAGE_FRAGMENT_DENSITY_PROCESS_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04079) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04079

If the [`transformFeedback`](features.html#features-transformFeedback) feature
is not enabled, `pipelineStage` **must** not be
`VK_PIPELINE_STAGE_TRANSFORM_FEEDBACK_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04080) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-04080

If the [`meshShader`](features.html#features-meshShader) feature is not enabled,
`pipelineStage` **must** not be
`VK_PIPELINE_STAGE_MESH_SHADER_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-07077) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-07077

If the [`taskShader`](features.html#features-taskShader) feature is not enabled,
`pipelineStage` **must** not be
`VK_PIPELINE_STAGE_TASK_SHADER_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-shadingRateImage-07314) VUID-vkCmdWriteBufferMarkerAMD-shadingRateImage-07314

If neither of the [`shadingRateImage`](features.html#features-shadingRateImage)
or the [    `attachmentFragmentShadingRate`](features.html#features-attachmentFragmentShadingRate) features are enabled,
`pipelineStage` **must** not be
`VK_PIPELINE_STAGE_FRAGMENT_SHADING_RATE_ATTACHMENT_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-synchronization2-06489) VUID-vkCmdWriteBufferMarkerAMD-synchronization2-06489

If the [`synchronization2`](features.html#features-synchronization2) feature is
not enabled, `pipelineStage` **must** not be
`VK_PIPELINE_STAGE_NONE`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-rayTracingPipeline-07943) VUID-vkCmdWriteBufferMarkerAMD-rayTracingPipeline-07943

If neither of the [VK_NV_ray_tracing](../appendices/extensions.html#VK_NV_ray_tracing) extension or the
[`rayTracingPipeline`](features.html#features-rayTracingPipeline) feature are
enabled, `pipelineStage` **must** not be
`VK_PIPELINE_STAGE_RAY_TRACING_SHADER_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-dstOffset-01798) VUID-vkCmdWriteBufferMarkerAMD-dstOffset-01798

`dstOffset` **must** be less than or equal to the size of
`dstBuffer` minus `4`

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-dstBuffer-01799) VUID-vkCmdWriteBufferMarkerAMD-dstBuffer-01799

`dstBuffer` **must** have been created with
`VK_BUFFER_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-dstBuffer-01800) VUID-vkCmdWriteBufferMarkerAMD-dstBuffer-01800

If `dstBuffer` is non-sparse then it **must** be bound completely and
contiguously to a single `VkDeviceMemory` object

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-dstOffset-01801) VUID-vkCmdWriteBufferMarkerAMD-dstOffset-01801

`dstOffset` **must** be a multiple of `4`

Valid Usage (Implicit)

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-commandBuffer-parameter) VUID-vkCmdWriteBufferMarkerAMD-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-parameter) VUID-vkCmdWriteBufferMarkerAMD-pipelineStage-parameter

 If `pipelineStage` is not `0`, `pipelineStage` **must** be a valid [VkPipelineStageFlagBits](synchronization.html#VkPipelineStageFlagBits) value

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-dstBuffer-parameter) VUID-vkCmdWriteBufferMarkerAMD-dstBuffer-parameter

 `dstBuffer` **must** be a valid [VkBuffer](resources.html#VkBuffer) handle

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-commandBuffer-recording) VUID-vkCmdWriteBufferMarkerAMD-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-commandBuffer-cmdpool) VUID-vkCmdWriteBufferMarkerAMD-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-videocoding) VUID-vkCmdWriteBufferMarkerAMD-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdWriteBufferMarkerAMD-commonparent) VUID-vkCmdWriteBufferMarkerAMD-commonparent

 Both of `commandBuffer`, and `dstBuffer` **must** have been created, allocated, or retrieved from the same [VkDevice](devsandqueues.html#VkDevice)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Both
Outside
Transfer

Graphics

Compute
Action
