# VkRenderingEndInfoEXT(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkRenderingEndInfoEXT.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Members](#_members)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkRenderingEndInfoEXT - Structure specifying render pass end information

The `VkRenderingEndInfoEXT` structure is defined as:

// Provided by VK_EXT_fragment_density_map_offset
typedef struct VkRenderingEndInfoEXT {
    VkStructureType    sType;
    const void*        pNext;
} VkRenderingEndInfoEXT;

* 
`sType` is a [VkStructureType](VkStructureType.html) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

Valid Usage (Implicit)

* 
[](#VUID-VkRenderingEndInfoEXT-sType-sType) VUID-VkRenderingEndInfoEXT-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_RENDERING_END_INFO_EXT`

* 
[](#VUID-VkRenderingEndInfoEXT-pNext-pNext) VUID-VkRenderingEndInfoEXT-pNext-pNext

 `pNext` **must** be `NULL` or a pointer to a valid instance of [VkRenderPassFragmentDensityMapOffsetEndInfoEXT](VkRenderPassFragmentDensityMapOffsetEndInfoEXT.html)

* 
[](#VUID-VkRenderingEndInfoEXT-sType-unique) VUID-VkRenderingEndInfoEXT-sType-unique

 The `sType` value of each structure in the `pNext` chain **must** be unique

[VK_EXT_fragment_density_map_offset](VK_EXT_fragment_density_map_offset.html), [VkStructureType](VkStructureType.html), [vkCmdEndRendering2EXT](vkCmdEndRendering2EXT.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/renderpass.html#VkRenderingEndInfoEXT).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
