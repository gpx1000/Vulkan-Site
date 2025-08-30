# Deprecation

## Metadata

- **Component**: spec
- **Version**: latest
- **URL**: /spec/latest/appendices/deprecation.html

## Table of Contents

- [Deprecated Functionality](#_deprecated_functionality)
- [Physical Device Queries: Deprecation via version 2](#deprecation-gpdp2)
- [Physical_Device_Queries:_Deprecation_via_version_2](#deprecation-gpdp2)
- [Version Macros: Deprecation via replacements including API variant](#deprecation-version-macros)
- [Version_Macros:_Deprecation_via_replacements_including_API_variant](#deprecation-version-macros)
- [Device Layers: Deprecation via instance layers](#deprecation-devicelayers)
- [Device_Layers:_Deprecation_via_instance_layers](#deprecation-devicelayers)
- [Render Pass Functions: Deprecation via version 2](#deprecation-renderpass2)
- [Render_Pass_Functions:_Deprecation_via_version_2](#deprecation-renderpass2)
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

|  | Deprecation is tagged in the xml registry, with both core versions and
| --- | --- |
extensions able to express deprecation of any other interface.
All deprecations will be listed in this section, however only functionality
deprecated by a core version that is present will be emphasized with
warnings. |

Deprecated functionality is **not** removed from the specification, such that
older applications will continue to run on the same API for its lifetime.
Applications **may** wish to avoid deprecated functionality in favor of other
solutions.
Interactions with deprecated functionality will often be omitted when new
extensions or features are developed, so deprecated functionality may not
work with the latest features.

|  | Extensions can be deprecated in their entirety by a different mechanism, and
| --- | --- |
are marked as deprecated in their appendix.
See [the Deprecation section of the Extensions chapter](../chapters/extensions.html#extendingvulkan-compatibility-deprecation) for more information. |

When functionality is deprecated, an explanation of its deprecation will be
added to the below sections.

|  | This list is a work in progress - we intend to add other items to this
| --- | --- |
section over time; things such as shader modules (deprecated by
[VK_KHR_maintenance5](extensions.html#VK_KHR_maintenance5)) and anything superseded by a new version of the
same functionality (e.g. [VK_KHR_synchronization2](extensions.html#VK_KHR_synchronization2)). |

[VK_KHR_get_physical_device_properties2](extensions.html#VK_KHR_get_physical_device_properties2) was incorporated into Vulkan
1.1, which introduced new versions of several physical device query
functions.
These provide the same functionality as the Vulkan 1.0 functionality but
with greater extensibility.

When querying device features, [vkGetPhysicalDeviceFeatures2](../chapters/features.html#vkGetPhysicalDeviceFeatures2) **should** be
used instead of [vkGetPhysicalDeviceFeatures](../chapters/features.html#vkGetPhysicalDeviceFeatures).
When enabling device features, [VkPhysicalDeviceFeatures2](../chapters/features.html#VkPhysicalDeviceFeatures2) **should** be
provided in the `pNext` chain of [VkDeviceCreateInfo](../chapters/devsandqueues.html#VkDeviceCreateInfo) instead of
using [VkDeviceCreateInfo](../chapters/devsandqueues.html#VkDeviceCreateInfo)::pNext:pEnabledFeatures.

The version macros that do not take the API variant into account, such as
[VK_MAKE_VERSION](../chapters/extensions.html#VK_MAKE_VERSION) or [VK_VERSION_MAJOR](../chapters/extensions.html#VK_VERSION_MAJOR), are deprecated by those
that do, such as [VK_MAKE_API_VERSION](../chapters/extensions.html#VK_MAKE_API_VERSION) or [VK_API_VERSION_MAJOR](../chapters/extensions.html#VK_API_VERSION_MAJOR).

Instead of [VK_API_VERSION](boilerplate.html#VK_API_VERSION), specific version defines (e.g.
[VK_API_VERSION_1_0](../chapters/extensions.html#VK_API_VERSION_1_0)) or the [VK_MAKE_API_VERSION](../chapters/extensions.html#VK_MAKE_API_VERSION) macro should be
used instead.

Previous versions of this specification distinguished between instance and
device layers.
Instance layers were only able to intercept commands that operate on
`VkInstance` and `VkPhysicalDevice`, except they were not able to
intercept [vkCreateDevice](../chapters/devsandqueues.html#vkCreateDevice).
Device layers were enabled for individual devices when they were created,
and could only intercept commands operating on that device or its child
objects.

Device-only layers are now deprecated, and this specification no longer
distinguishes between instance and device layers.
Layers are enabled during instance creation, and are able to intercept all
commands operating on that instance or any of its child objects.
At the time of deprecation there were no known device-only layers and no
compelling reason to create one.

[VK_KHR_create_renderpass2](extensions.html#VK_KHR_create_renderpass2) was incorporated into Vulkan 1.2, which
introduced new versions of several render pass functions.
These provide the same functionality as the Vulkan 1.0 functionality but
with greater extensibility.

|  | Render pass objects and all related commands are further
| --- | --- |
[deprecated by dynamic rendering](#deprecation-dynamicrendering) in Vulkan
1.4. |

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

|  | [VK_QCOM_render_pass_shader_resolve](extensions.html#VK_QCOM_render_pass_shader_resolve) does not have equivalent
| --- | --- |
functionality exposed via dynamic rendering.
Use of deprecated functionality will be required to use that extension
unless/until replacements are created. |

Outside of vendor extensions, applications are advised to make use of
[vkCmdBeginRendering](../chapters/renderpass.html#vkCmdBeginRendering) and [vkCmdEndRendering](../chapters/renderpass.html#vkCmdEndRendering) to manage render
passes from this API version onward.
