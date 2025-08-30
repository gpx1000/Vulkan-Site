# VkDecompressMemoryRegionNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkDecompressMemoryRegionNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Members](#_members)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkDecompressMemoryRegionNV - Structure specifying decompression parameters

The `VkDecompressMemoryRegionNV` structure is defined as:

// Provided by VK_NV_memory_decompression
typedef struct VkDecompressMemoryRegionNV {
    VkDeviceAddress                       srcAddress;
    VkDeviceAddress                       dstAddress;
    VkDeviceSize                          compressedSize;
    VkDeviceSize                          decompressedSize;
    VkMemoryDecompressionMethodFlagsNV    decompressionMethod;
} VkDecompressMemoryRegionNV;

* 
`srcAddress` is the address where compressed data is stored.

* 
`dstAddress` is the destination address where decompressed data will
be written.

* 
`compressedSize` is the size of compressed data in bytes.

* 
`decompressedSize` is the size of decompressed data in bytes.

* 
`decompressionMethod` is a bitmask of
`VkMemoryDecompressionMethodFlagBitsNV` with a single bit set
specifying the method used to decompress data.

Valid Usage

* 
[](#VUID-VkDecompressMemoryRegionNV-srcAddress-07685) VUID-VkDecompressMemoryRegionNV-srcAddress-07685

The `srcAddress` **must** be 4 byte aligned

* 
[](#VUID-VkDecompressMemoryRegionNV-srcAddress-07686) VUID-VkDecompressMemoryRegionNV-srcAddress-07686

The memory in range `srcAddress` and `srcAddress` + 
`compressedSize` **must** be valid and bound to a `VkDeviceMemory`
object

* 
[](#VUID-VkDecompressMemoryRegionNV-dstAddress-07687) VUID-VkDecompressMemoryRegionNV-dstAddress-07687

The `dstAddress` **must** be 4 byte aligned

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-09395) VUID-VkDecompressMemoryRegionNV-decompressionMethod-09395

If `decompressionMethod` is
`VK_MEMORY_DECOMPRESSION_METHOD_GDEFLATE_1_0_BIT_NV`, then
`decompressedSize` **must** be less than or equal to 65536 bytes

* 
[](#VUID-VkDecompressMemoryRegionNV-dstAddress-07688) VUID-VkDecompressMemoryRegionNV-dstAddress-07688

The memory in range `dstAddress` and `dstAddress` + 
`decompressedSize` **must** be valid and bound to a
`VkDeviceMemory` object

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressedSize-07689) VUID-VkDecompressMemoryRegionNV-decompressedSize-07689

The `decompressedSize` **must** be large enough to hold the
decompressed data based on the `decompressionMethod`

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-07690) VUID-VkDecompressMemoryRegionNV-decompressionMethod-07690

The `decompressionMethod` **must** have a single bit set

* 
[](#VUID-VkDecompressMemoryRegionNV-srcAddress-07691) VUID-VkDecompressMemoryRegionNV-srcAddress-07691

The `srcAddress` to `srcAddress` +  `compressedSize`
region **must** not overlap with the `dstAddress` and `dstAddress`
+  `decompressedSize` region

Valid Usage (Implicit)

* 
[](#VUID-VkDecompressMemoryRegionNV-srcAddress-parameter) VUID-VkDecompressMemoryRegionNV-srcAddress-parameter

 `srcAddress` **must** be a valid `VkDeviceAddress` value

* 
[](#VUID-VkDecompressMemoryRegionNV-dstAddress-parameter) VUID-VkDecompressMemoryRegionNV-dstAddress-parameter

 `dstAddress` **must** be a valid `VkDeviceAddress` value

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-parameter) VUID-VkDecompressMemoryRegionNV-decompressionMethod-parameter

 `decompressionMethod` **must** be a valid combination of [VkMemoryDecompressionMethodFlagBitsNV](VkMemoryDecompressionMethodFlagBitsNV.html) values

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-requiredbitmask) VUID-VkDecompressMemoryRegionNV-decompressionMethod-requiredbitmask

 `decompressionMethod` **must** not be `0`

[VK_NV_memory_decompression](VK_NV_memory_decompression.html), `VkDeviceAddress`, `VkDeviceSize`, [VkMemoryDecompressionMethodFlagsNV](VkMemoryDecompressionMethodFlagsNV.html), [vkCmdDecompressMemoryNV](vkCmdDecompressMemoryNV.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/VK_NV_memory_decompression.html#VkDecompressMemoryRegionNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
