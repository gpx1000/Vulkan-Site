# VkCopyMemoryIndirectCommandNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkCopyMemoryIndirectCommandNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Members](#_members)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkCopyMemoryIndirectCommandNV - Structure specifying indirect memory region copy operation

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

Valid Usage (Implicit)

* 
[](#VUID-VkCopyMemoryIndirectCommandNV-srcAddress-parameter) VUID-VkCopyMemoryIndirectCommandNV-srcAddress-parameter

 `srcAddress` **must** be a valid `VkDeviceAddress` value

* 
[](#VUID-VkCopyMemoryIndirectCommandNV-dstAddress-parameter) VUID-VkCopyMemoryIndirectCommandNV-dstAddress-parameter

 `dstAddress` **must** be a valid `VkDeviceAddress` value

[VK_NV_copy_memory_indirect](VK_NV_copy_memory_indirect.html), `VkDeviceAddress`, `VkDeviceSize`

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/copies.html#VkCopyMemoryIndirectCommandNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
