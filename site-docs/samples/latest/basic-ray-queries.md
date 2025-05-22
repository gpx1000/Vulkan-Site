# Basic ray queries

## Metadata

- **Component**: samples
- **Version**: latest
- **URL**: /samples/latest/samples/extensions/ray_queries/README.html

## Content

**Extensions**: [`VK_KHR_ray_query`](https://www.khronos.org/registry/vulkan/specs/1.2-extensions/html/vkspec.html#VK_KHR_ray_query), [`VK_KHR_acceleration_structure`](https://www.khronos.org/registry/vulkan/specs/1.2-extensions/html/vkspec.html#VK_KHR_acceleration_structure)

Render a sponza scene using the ray query extension.
Shows how to set up all data structures required for ray queries, including the bottom and top level acceleration structures for the geometry and a standard vertex/fragment shader pipeline.
Shadows are cast dynamically by ray queries being cast by the fragment shader.
