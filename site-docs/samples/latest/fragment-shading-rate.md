# Fragment shading rate

## Metadata

- **Component**: samples
- **Version**: latest
- **URL**: /samples/latest/samples/extensions/fragment_shading_rate/README.html

## Content

|  | The source for this sample can be found in the [Khronos Vulkan samples github repository](https://github.com/KhronosGroup/Vulkan-Samples/tree/main/samples/extensions/fragment_shading_rate). |
| --- | --- |

**Extension**: [`VK_KHR_fragment_shading_rate`](https://www.khronos.org/registry/vulkan/specs/1.2-extensions/man/html/VK_KHR_fragment_shading_rate.html)

Uses a special framebuffer attachment to control fragment shading rates for different framebuffer regions.
This allows explicit control over the number of fragment shader invocations for each pixel covered by a fragment, which is e.g.
useful for foveated rendering.
