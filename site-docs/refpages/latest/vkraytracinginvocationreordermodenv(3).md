# VkRayTracingInvocationReorderModeNV(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/VkRayTracingInvocationReorderModeNV.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

VkRayTracingInvocationReorderModeNV - Enum providing a hint on how the application **may** reorder

Values which **may** be returned in the
`rayTracingInvocationReorderReorderingHint` field of
`VkPhysicalDeviceRayTracingInvocationReorderPropertiesNV` are:

// Provided by VK_NV_ray_tracing_invocation_reorder
typedef enum VkRayTracingInvocationReorderModeNV {
    VK_RAY_TRACING_INVOCATION_REORDER_MODE_NONE_NV = 0,
    VK_RAY_TRACING_INVOCATION_REORDER_MODE_REORDER_NV = 1,
} VkRayTracingInvocationReorderModeNV;

* 
`VK_RAY_TRACING_INVOCATION_REORDER_MODE_NONE_NV` specifies that the
implementation is likely to not reorder at reorder calls.

* 
`VK_RAY_TRACING_INVOCATION_REORDER_MODE_REORDER_NV` specifies that
the implementation is likely to reorder at reorder calls.

[VK_NV_ray_tracing_invocation_reorder](VK_NV_ray_tracing_invocation_reorder.html), [VkPhysicalDeviceRayTracingInvocationReorderPropertiesNV](VkPhysicalDeviceRayTracingInvocationReorderPropertiesNV.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/limits.html#VkRayTracingInvocationReorderModeNV).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
