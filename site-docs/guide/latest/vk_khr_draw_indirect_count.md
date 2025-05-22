# VK_KHR_draw_indirect_count

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/extensions/VK_KHR_draw_indirect_count.html

## Content

Every call to `vkCmdDraw` consumes a set of parameters describing the draw call. To batch draw calls together the same parameters are stored in a `VkBuffer` in blocks of `VkDrawIndirectCommand`. Using `vkCmdDrawIndirect` allows you to invoke a `drawCount` number of draws, but the `drawCount` is needed at record time. The new `vkCmdDrawIndirectCount` call allows the `drawCount` to also be in a `VkBuffer`. This allows the value of `drawCount` to be dynamic and decided when the draw call is executed.

The following diagram is to visualize the difference between `vkCmdDraw`, `vkCmdDrawIndirect`, and `vkCmdDrawIndirectCount`.

![VK_KHR_draw_indirect_count example](../_images/extensions/VK_KHR_draw_indirect_count_example.png)
