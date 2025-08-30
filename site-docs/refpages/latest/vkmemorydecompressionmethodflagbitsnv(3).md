# VkMemoryDecompressionMethodFlagBitsNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkMemoryDecompressionMethodFlagBitsNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkMemoryDecompressionMethodFlagBitsNV - List the supported memory decompression methods

Bits which **can** be set in
`VkDecompressMemoryRegionNV`::`decompressionMethod` specifying the
decompression method to select, or returned in
`VkPhysicalDeviceMemoryDecompressionPropertiesNV`::`decompressionMethods`
specifying the available decompression methods are:

// Provided by VK_NV_memory_decompression
// Flag bits for VkMemoryDecompressionMethodFlagBitsNV
typedef VkFlags64 VkMemoryDecompressionMethodFlagBitsNV;
static const VkMemoryDecompressionMethodFlagBitsNV VK_MEMORY_DECOMPRESSION_METHOD_GDEFLATE_1_0_BIT_NV = 0x00000001ULL;

* 
`VK_MEMORY_DECOMPRESSION_METHOD_GDEFLATE_1_0_BIT_NV` specifies that
the GDeflate 1.0 algorithm is used to decompress data.

[VK_NV_memory_decompression](VK_NV_memory_decompression.html), [VkMemoryDecompressionMethodFlagsNV](VkMemoryDecompressionMethodFlagsNV.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/VK_NV_memory_decompression.html#VkMemoryDecompressionMethodFlagBitsNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
