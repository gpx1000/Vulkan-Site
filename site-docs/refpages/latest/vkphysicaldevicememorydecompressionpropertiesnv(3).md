# VkPhysicalDeviceMemoryDecompressionPropertiesNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkPhysicalDeviceMemoryDecompressionPropertiesNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Members](#_members)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkPhysicalDeviceMemoryDecompressionPropertiesNV - Structure describing supported memory decompression methods by an implementation

The `VkPhysicalDeviceMemoryDecompressionPropertiesNV` structure is
defined as:

// Provided by VK_NV_memory_decompression
typedef struct VkPhysicalDeviceMemoryDecompressionPropertiesNV {
    VkStructureType                       sType;
    void*                                 pNext;
    VkMemoryDecompressionMethodFlagsNV    decompressionMethods;
    uint64_t                              maxDecompressionIndirectCount;
} VkPhysicalDeviceMemoryDecompressionPropertiesNV;

* 
`sType` is a [VkStructureType](VkStructureType.html) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`decompressionMethods` is a bitmask of
[VkMemoryDecompressionMethodFlagBitsNV](VkMemoryDecompressionMethodFlagBitsNV.html) specifying memory
decompression methods supported by the implementation.

* 
`maxDecompressionIndirectCount` specifies the maximum supported
count value in the `countBuffer` of
[vkCmdDecompressMemoryIndirectCountNV](vkCmdDecompressMemoryIndirectCountNV.html)

If the `VkPhysicalDeviceMemoryDecompressionPropertiesNV` structure is included in the `pNext` chain of the
[VkPhysicalDeviceProperties2](VkPhysicalDeviceProperties2.html) structure passed to
[vkGetPhysicalDeviceProperties2](vkGetPhysicalDeviceProperties2.html), it is filled in with each
corresponding implementation-dependent property.

Valid Usage (Implicit)

* 
[](#VUID-VkPhysicalDeviceMemoryDecompressionPropertiesNV-sType-sType) VUID-VkPhysicalDeviceMemoryDecompressionPropertiesNV-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_PHYSICAL_DEVICE_MEMORY_DECOMPRESSION_PROPERTIES_NV`

[VK_NV_memory_decompression](VK_NV_memory_decompression.html), [VkMemoryDecompressionMethodFlagsNV](VkMemoryDecompressionMethodFlagsNV.html), [VkStructureType](VkStructureType.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/limits.html#VkPhysicalDeviceMemoryDecompressionPropertiesNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
