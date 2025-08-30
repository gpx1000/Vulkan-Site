# VkPhysicalDeviceCopyMemoryIndirectPropertiesNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkPhysicalDeviceCopyMemoryIndirectPropertiesNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Members](#_members)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkPhysicalDeviceCopyMemoryIndirectPropertiesNV - Structure describing supported queues for indirect copy

The `VkPhysicalDeviceCopyMemoryIndirectPropertiesNV` structure is
defined as:

// Provided by VK_NV_copy_memory_indirect
typedef struct VkPhysicalDeviceCopyMemoryIndirectPropertiesNV {
    VkStructureType    sType;
    void*              pNext;
    VkQueueFlags       supportedQueues;
} VkPhysicalDeviceCopyMemoryIndirectPropertiesNV;

* 
`sType` is a [VkStructureType](VkStructureType.html) value identifying this structure.

* 
`pNext` is `NULL` or a pointer to a structure extending this
structure.

* 
`supportedQueues` is a bitmask of [VkQueueFlagBits](VkQueueFlagBits.html) indicating
the queues on which [indirect copy commands](../../../../spec/latest/chapters/copies.html#indirect-copies) are
supported.

If the [`indirectCopy`](../../../../spec/latest/chapters/features.html#features-indirectCopy) feature is supported,
`supportedQueues` **must** return at least one supported queue.

If the `VkPhysicalDeviceCopyMemoryIndirectPropertiesNV` structure is included in the `pNext` chain of the
[VkPhysicalDeviceProperties2](VkPhysicalDeviceProperties2.html) structure passed to
[vkGetPhysicalDeviceProperties2](vkGetPhysicalDeviceProperties2.html), it is filled in with each
corresponding implementation-dependent property.

Valid Usage (Implicit)

* 
[](#VUID-VkPhysicalDeviceCopyMemoryIndirectPropertiesNV-sType-sType) VUID-VkPhysicalDeviceCopyMemoryIndirectPropertiesNV-sType-sType

 `sType` **must** be `VK_STRUCTURE_TYPE_PHYSICAL_DEVICE_COPY_MEMORY_INDIRECT_PROPERTIES_NV`

[VK_NV_copy_memory_indirect](VK_NV_copy_memory_indirect.html), [VkQueueFlags](VkQueueFlags.html), [VkStructureType](VkStructureType.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/limits.html#VkPhysicalDeviceCopyMemoryIndirectPropertiesNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
