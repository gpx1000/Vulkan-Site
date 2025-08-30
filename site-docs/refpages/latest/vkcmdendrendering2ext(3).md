# vkCmdEndRendering2EXT(3)

## Metadata

- **Component**: refpages
- **Version**: latest
- **URL**: /refpages/latest/refpages/source/vkCmdEndRendering2EXT.html

## Table of Contents

- [Name](#_name)
- [C Specification](#_c_specification)
- [Parameters](#_parameters)
- [Description](#_description)
- [See Also](#_see_also)
- [Document Notes](#_document_notes)

## Content

vkCmdEndRendering2EXT - End a dynamic render pass instance

Alternatively, to end a render pass instance, call:

// Provided by VK_EXT_fragment_density_map_offset
void vkCmdEndRendering2EXT(
    VkCommandBuffer                             commandBuffer,
    const VkRenderingEndInfoEXT*                pRenderingEndInfo);

* 
`commandBuffer` is the command buffer in which to record the
command.

* 
`pRenderingEndInfo` is `NULL` or a pointer to a
[VkRenderingEndInfoEXT](VkRenderingEndInfoEXT.html) structure containing information about how
the render pass will be ended.

If the value of `pRenderingInfo->flags` used to begin this render pass
instance included `VK_RENDERING_SUSPENDING_BIT`, then this render pass
is suspended and will be resumed later in
[submission order](../../../../spec/latest/chapters/synchronization.html#synchronization-submission-order).

Valid Usage

* 
[](#VUID-vkCmdEndRendering2EXT-None-10610) VUID-vkCmdEndRendering2EXT-None-10610

The current render pass instance **must** have been begun with
[vkCmdBeginRendering](vkCmdBeginRendering.html)

* 
[](#VUID-vkCmdEndRendering2EXT-commandBuffer-10611) VUID-vkCmdEndRendering2EXT-commandBuffer-10611

The current render pass instance **must** have been begun in
`commandBuffer`

* 
[](#VUID-vkCmdEndRendering2EXT-None-10612) VUID-vkCmdEndRendering2EXT-None-10612

This command **must** not be recorded when transform feedback is active

* 
[](#VUID-vkCmdEndRendering2EXT-None-10613) VUID-vkCmdEndRendering2EXT-None-10613

If `vkCmdBeginQuery`* was called within the render pass, the
corresponding `vkCmdEndQuery`* **must** have been called subsequently
within the same subpass

Valid Usage (Implicit)

* 
[](#VUID-vkCmdEndRendering2EXT-commandBuffer-parameter) VUID-vkCmdEndRendering2EXT-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](VkCommandBuffer.html) handle

* 
[](#VUID-vkCmdEndRendering2EXT-pRenderingEndInfo-parameter) VUID-vkCmdEndRendering2EXT-pRenderingEndInfo-parameter

 If `pRenderingEndInfo` is not `NULL`, `pRenderingEndInfo` **must** be a valid pointer to a valid [VkRenderingEndInfoEXT](VkRenderingEndInfoEXT.html) structure

* 
[](#VUID-vkCmdEndRendering2EXT-commandBuffer-recording) VUID-vkCmdEndRendering2EXT-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](../../../../spec/latest/chapters/cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdEndRendering2EXT-commandBuffer-cmdpool) VUID-vkCmdEndRendering2EXT-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics operations

* 
[](#VUID-vkCmdEndRendering2EXT-renderpass) VUID-vkCmdEndRendering2EXT-renderpass

 This command **must** only be called inside of a render pass instance

* 
[](#VUID-vkCmdEndRendering2EXT-videocoding) VUID-vkCmdEndRendering2EXT-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties
| [Command Buffer Levels](../../../../spec/latest/chapters/cmdbuffers.html#VkCommandBufferLevel) | [Render Pass Scope](../../../../spec/latest/chapters/renderpass.html#vkCmdBeginRenderPass) | [Video Coding Scope](../../../../spec/latest/chapters/videocoding.html#vkCmdBeginVideoCodingKHR) | [Supported Queue Types](../../../../spec/latest/chapters/devsandqueues.html#VkQueueFlagBits) | [Command Type](../../../../spec/latest/chapters/fundamentals.html#fundamentals-queueoperation-command-types) |
| --- | --- | --- | --- | --- |
| Primary

Secondary | Inside | Outside | Graphics | Action

State |

Conditional Rendering

vkCmdEndRendering2EXT is not affected by [conditional rendering](../../../../spec/latest/chapters/drawing.html#drawing-conditional-rendering)

[VK_EXT_fragment_density_map_offset](VK_EXT_fragment_density_map_offset.html), [VkCommandBuffer](VkCommandBuffer.html), [VkRenderingEndInfoEXT](VkRenderingEndInfoEXT.html)

For more information, see the [Vulkan Specification](../../../../spec/latest/chapters/renderpass.html#vkCmdEndRendering2EXT).

This page is extracted from the Vulkan Specification.
Fixes and changes should be made to the Specification, not directly.
