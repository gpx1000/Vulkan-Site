# VkResolveImageInfo2(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkResolveImageInfo2.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Members](#_members)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkResolveImageInfo2 - Structure specifying parameters of resolve image command

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
`sType` is a [VkStructureType](VkStructureType.html) value identifying this structure.

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
`pRegions` is a pointer to an array of [VkImageResolve2](VkImageResolve2.html)
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

The [format features](../../../../spec/latest/chapters/resources.html#resources-image-format-features) of
`dstImage` **must** contain
`VK_FORMAT_FEATURE_COLOR_ATTACHMENT_BIT`

* 
[](#VUID-VkResolveImageInfo2-linearColorAttachment-06519) VUID-VkResolveImageInfo2-linearColorAttachment-06519

If the [`linearColorAttachment`](../../../../spec/latest/chapters/features.html#features-linearColorAttachment)
feature is enabled and the image is created with
`VK_IMAGE_TILING_LINEAR`, the
[format features](../../../../spec/latest/chapters/resources.html#resources-image-format-features) of `dstImage`
**must** contain `VK_FORMAT_FEATURE_2_LINEAR_COLOR_ATTACHMENT_BIT_NV`

* 
[](#VUID-VkResolveImageInfo2-srcImage-01386) VUID-VkResolveImageInfo2-srcImage-01386

`srcImage` and `dstImage` **must** have been created with the same
image format

* 
[](#VUID-VkResolveImageInfo2-srcSubresource-01709) VUID-VkResolveImageInfo2-srcSubresource-01709

The `srcSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](VkImageCreateInfo.html) when `srcImage` was created

* 
[](#VUID-VkResolveImageInfo2-dstSubresource-01710) VUID-VkResolveImageInfo2-dstSubresource-01710

The `dstSubresource.mipLevel` member of each element of
`pRegions` **must** be less than the `mipLevels` specified in
[VkImageCreateInfo](VkImageCreateInfo.html) when `dstImage` was created

* 
[](#VUID-VkResolveImageInfo2-srcSubresource-01711) VUID-VkResolveImageInfo2-srcSubresource-01711

If `srcSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`srcSubresource.baseArrayLayer` + 
`srcSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](VkImageCreateInfo.html) when `srcImage` was created

* 
[](#VUID-VkResolveImageInfo2-dstSubresource-01712) VUID-VkResolveImageInfo2-dstSubresource-01712

If `dstSubresource.layerCount` is not
`VK_REMAINING_ARRAY_LAYERS`,
`dstSubresource.baseArrayLayer` + 
`dstSubresource.layerCount` of each element of `pRegions` **must**
be less than or equal to the `arrayLayers` specified in
[VkImageCreateInfo](VkImageCreateInfo.html) when `dstImage` was created

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

The [format features](../../../../spec/latest/chapters/resources.html#resources-image-format-features) of
`srcImage` **must** contain `VK_FORMAT_FEATURE_TRANSFER_SRC_BIT`

* 
[](#VUID-VkResolveImageInfo2-dstImage-06764) VUID-VkResolveImageInfo2-dstImage-06764

`dstImage` **must** have been created with
`VK_IMAGE_USAGE_TRANSFER_DST_BIT` usage flag

* 
[](#VUID-VkResolveImageInfo2-dstImage-06765) VUID-VkResolveImageInfo2-dstImage-06765

The [format features](../../../../spec/latest/chapters/resources.html#resources-image-format-features) of
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

 `srcImage` **must** be a valid [VkImage](VkImage.html) handle

* 
[](#VUID-VkResolveImageInfo2-srcImageLayout-parameter) VUID-VkResolveImageInfo2-srcImageLayout-parameter

 `srcImageLayout` **must** be a valid [VkImageLayout](VkImageLayout.html) value

* 
[](#VUID-VkResolveImageInfo2-dstImage-parameter) VUID-VkResolveImageInfo2-dstImage-parameter

 `dstImage` **must** be a valid [VkImage](VkImage.html) handle

* 
[](#VUID-VkResolveImageInfo2-dstImageLayout-parameter) VUID-VkResolveImageInfo2-dstImageLayout-parameter

 `dstImageLayout` **must** be a valid [VkImageLayout](VkImageLayout.html) value

* 
[](#VUID-VkResolveImageInfo2-pRegions-parameter) VUID-VkResolveImageInfo2-pRegions-parameter

 `pRegions` **must** be a valid pointer to an array of `regionCount` valid [VkImageResolve2](VkImageResolve2.html) structures

* 
[](#VUID-VkResolveImageInfo2-regionCount-arraylength) VUID-VkResolveImageInfo2-regionCount-arraylength

 `regionCount` **must** be greater than `0`

* 
[](#VUID-VkResolveImageInfo2-commonparent) VUID-VkResolveImageInfo2-commonparent

 Both of `dstImage`, and `srcImage` **must** have been created, allocated, or retrieved from the same [VkDevice](VkDevice.html)

[VK_KHR_copy_commands2](VK_KHR_copy_commands2.html), [VK_VERSION_1_3](VK_VERSION_1_3.html), [VkImage](VkImage.html), [VkImageLayout](VkImageLayout.html), [VkImageResolve2](VkImageResolve2.html), [VkStructureType](VkStructureType.html), [vkCmdResolveImage2](vkCmdResolveImage2.html), [vkCmdResolveImage2](vkCmdResolveImage2.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/copies.html#VkResolveImageInfo2).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
