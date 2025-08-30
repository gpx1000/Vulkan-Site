# vkCmdWriteBufferMarker2AMD(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/vkCmdWriteBufferMarker2AMD.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Parameters](#_parameters)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

vkCmdWriteBufferMarker2AMD - Execute a pipelined write of a marker value into a buffer

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

|  | Similar to `vkCmdWriteTimestamp2`, if an implementation is unable to
| --- | --- |
write a marker at any specific pipeline stage, it **may** instead do so at any
logically later stage. |

|  | Implementations **may** only support a limited number of pipelined marker write
| --- | --- |
operations in flight at a given time.
Thus an excessive number of marker write operations **may** degrade command
execution performance. |

Valid Usage

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03929) VUID-vkCmdWriteBufferMarker2AMD-stage-03929

If the [`geometryShader`](../../../../spec/latest/chapters/features.html#features-geometryShader) feature is not
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_GEOMETRY_SHADER_BIT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03930) VUID-vkCmdWriteBufferMarker2AMD-stage-03930

If the [`tessellationShader`](../../../../spec/latest/chapters/features.html#features-tessellationShader) feature
is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_TESSELLATION_CONTROL_SHADER_BIT` or
`VK_PIPELINE_STAGE_2_TESSELLATION_EVALUATION_SHADER_BIT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03931) VUID-vkCmdWriteBufferMarker2AMD-stage-03931

If the [`conditionalRendering`](../../../../spec/latest/chapters/features.html#features-conditionalRendering)
feature is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_CONDITIONAL_RENDERING_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03932) VUID-vkCmdWriteBufferMarker2AMD-stage-03932

If the [`fragmentDensityMap`](../../../../spec/latest/chapters/features.html#features-fragmentDensityMap) feature
is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_FRAGMENT_DENSITY_PROCESS_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03933) VUID-vkCmdWriteBufferMarker2AMD-stage-03933

If the [`transformFeedback`](../../../../spec/latest/chapters/features.html#features-transformFeedback) feature
is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_TRANSFORM_FEEDBACK_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03934) VUID-vkCmdWriteBufferMarker2AMD-stage-03934

If the [`meshShader`](../../../../spec/latest/chapters/features.html#features-meshShader) feature is not enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_MESH_SHADER_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-03935) VUID-vkCmdWriteBufferMarker2AMD-stage-03935

If the [`taskShader`](../../../../spec/latest/chapters/features.html#features-taskShader) feature is not enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_TASK_SHADER_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-07316) VUID-vkCmdWriteBufferMarker2AMD-stage-07316

If neither of the [`shadingRateImage`](../../../../spec/latest/chapters/features.html#features-shadingRateImage)
or the [    `attachmentFragmentShadingRate`](../../../../spec/latest/chapters/features.html#features-attachmentFragmentShadingRate) features are enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_FRAGMENT_SHADING_RATE_ATTACHMENT_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-04957) VUID-vkCmdWriteBufferMarker2AMD-stage-04957

If the [`subpassShading`](../../../../spec/latest/chapters/features.html#features-subpassShading) feature is not
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_SUBPASS_SHADER_BIT_HUAWEI`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-04995) VUID-vkCmdWriteBufferMarker2AMD-stage-04995

If the [`invocationMask`](../../../../spec/latest/chapters/features.html#features-invocationMask) feature is not
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_INVOCATION_MASK_BIT_HUAWEI`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-07946) VUID-vkCmdWriteBufferMarker2AMD-stage-07946

If neither the [VK_NV_ray_tracing](VK_NV_ray_tracing.html) extension or the
[`rayTracingPipeline`](../../../../spec/latest/chapters/features.html#features-rayTracingPipeline) feature are
enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_RAY_TRACING_SHADER_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-10751) VUID-vkCmdWriteBufferMarker2AMD-stage-10751

If the [`accelerationStructure`](../../../../spec/latest/chapters/features.html#features-accelerationStructure)
feature is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_ACCELERATION_STRUCTURE_BUILD_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-10752) VUID-vkCmdWriteBufferMarker2AMD-stage-10752

If the [`rayTracingMaintenance1`](../../../../spec/latest/chapters/features.html#features-rayTracingMaintenance1)
feature is not enabled, `stage` **must** not contain
`VK_PIPELINE_STAGE_2_ACCELERATION_STRUCTURE_COPY_BIT_KHR`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-10753) VUID-vkCmdWriteBufferMarker2AMD-stage-10753

If the [`micromap`](../../../../spec/latest/chapters/features.html#features-micromap) feature is not enabled,
`stage` **must** not contain
`VK_PIPELINE_STAGE_2_MICROMAP_BUILD_BIT_EXT`

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-synchronization2-03893) VUID-vkCmdWriteBufferMarker2AMD-synchronization2-03893

The [`synchronization2`](../../../../spec/latest/chapters/features.html#features-synchronization2) feature **must**
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

 `commandBuffer` **must** be a valid [VkCommandBuffer](VkCommandBuffer.html) handle

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-stage-parameter) VUID-vkCmdWriteBufferMarker2AMD-stage-parameter

 `stage` **must** be a valid combination of [VkPipelineStageFlagBits2](VkPipelineStageFlagBits2.html) values

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-parameter) VUID-vkCmdWriteBufferMarker2AMD-dstBuffer-parameter

 `dstBuffer` **must** be a valid [VkBuffer](VkBuffer.html) handle

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-recording) VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](../../../../spec/latest/chapters/cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-cmdpool) VUID-vkCmdWriteBufferMarker2AMD-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support transfer, graphics, or compute operations

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-videocoding) VUID-vkCmdWriteBufferMarker2AMD-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdWriteBufferMarker2AMD-commonparent) VUID-vkCmdWriteBufferMarker2AMD-commonparent

 Both of `commandBuffer`, and `dstBuffer` **must** have been created, allocated, or retrieved from the same [VkDevice](VkDevice.html)

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties
| [Command Buffer Levels](../../../../spec/latest/chapters/cmdbuffers.html#VkCommandBufferLevel) | [Render Pass Scope](../../../../spec/latest/chapters/renderpass.html#vkCmdBeginRenderPass) | [Video Coding Scope](../../../../spec/latest/chapters/videocoding.html#vkCmdBeginVideoCodingKHR) | [Supported Queue Types](../../../../spec/latest/chapters/devsandqueues.html#VkQueueFlagBits) | [Command Type](../../../../spec/latest/chapters/fundamentals.html#fundamentals-queueoperation-command-types) |
| --- | --- | --- | --- | --- |
| Primary

Secondary | Both | Outside | Transfer

Graphics

Compute | Action |

Conditional Rendering

vkCmdWriteBufferMarker2AMD is not affected by [conditional rendering](../../../../spec/latest/chapters/drawing.html#drawing-conditional-rendering)

[VK_AMD_buffer_marker](VK_AMD_buffer_marker.html), [VK_KHR_synchronization2](VK_KHR_synchronization2.html), [VK_VERSION_1_3](VK_VERSION_1_3.html), [VkBuffer](VkBuffer.html), [VkCommandBuffer](VkCommandBuffer.html), `VkDeviceSize`, [VkPipelineStageFlags2](VkPipelineStageFlags2.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/copies.html#vkCmdWriteBufferMarker2AMD).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
