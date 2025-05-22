# Deprecation

## Metadata

- **Component**: spec
- **Version**: latest
- **URL**: /spec/latest/appendices/deprecation.html

## Table of Contents

- [Deprecated Functionality](#_deprecated_functionality)
- [Render Pass Objects: Deprecation via dynamic rendering](#_render_pass_objects_deprecation_via_dynamic_rendering)
- [Render_Pass_Objects:_Deprecation_via_dynamic_rendering](#_render_pass_objects_deprecation_via_dynamic_rendering)

## Content

Functionality in the specification such as commands and structures **may** be
marked as deprecated, indicating that applications **should** avoid using it.
A link to an explanatory section will be provided to explain how and why the
functionality was deprecated, what functionality replaces it (if any), and
what applications **should** do instead.
Reasons for deprecating functionality **may** include:

* 
Newer functionality fulfills the same role

* 
Does not work as originally intended

* 
Functionality cannot continue to work with newer features

Deprecated functionality will remain available for backwards compatibility
until a new major [core version](../chapters/extensions.html#extendingvulkan-compatibility-coreversions) removes it, but applications targeting more recent versions of
Vulkan **should** still avoid using deprecated functionality.
Interactions with deprecated functionality will often be omitted when new
extensions or features are developed, so deprecated functionality may not
work with the latest features.

When functionality is deprecated, an explanation of its deprecation will be
added to the below sections.

In Vulkan 1.3, the [VK_KHR_dynamic_rendering](extensions.html#VK_KHR_dynamic_rendering) extension was promoted
into core, which added a new way to specify render passes without needing to
create [VkFramebuffer](../chapters/renderpass.html#VkFramebuffer) and [VkRenderPass](../chapters/renderpass.html#VkRenderPass) objects.
However, subpass functionality had no equivalent, meaning dynamic rendering
was only suitable as a substitute for content not using subpasses.

In Vulkan 1.4 however, [VK_KHR_dynamic_rendering_local_read](extensions.html#VK_KHR_dynamic_rendering_local_read) was
promoted into core as well, which allows the expression of most subpass
functionality in core or extensions.
Any subpass functionality which was not replicated is still expressible but
requires applications to split work over multiple dynamic render pass
instances.
Functionality not covered with local reads would result in most or all
vendors splitting the subpass internally.

Outside of vendor extensions, applications are advised to make use of
[vkCmdBeginRendering](../chapters/renderpass.html#vkCmdBeginRendering) and [vkCmdEndRendering](../chapters/renderpass.html#vkCmdEndRendering) to manage render
passes from this API version onward.
