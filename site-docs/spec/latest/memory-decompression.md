# Memory Decompression

## Metadata

- **Component**: spec
- **Version**: latest
- **URL**: /spec/latest/chapters/VK_NV_memory_decompression.html

## Content

To decompress data between one or more memory regions call:

// Provided by VK_NV_memory_decompression
void vkCmdDecompressMemoryNV(
    VkCommandBuffer                             commandBuffer,
    uint32_t                                    decompressRegionCount,
    const VkDecompressMemoryRegionNV*           pDecompressMemoryRegions);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`decompressRegionCount` is the number of memory regions to
decompress.

* 
`pDecompressMemoryRegions` is a pointer to an array of
`decompressRegionCount` [VkDecompressMemoryRegionNV](#VkDecompressMemoryRegionNV) structures
specifying decompression parameters.

Each region specified in `pDecompressMemoryRegions` is decompressed from
the source to destination region based on the specified decompression
method.

Valid Usage

* 
[](#VUID-vkCmdDecompressMemoryNV-None-07684) VUID-vkCmdDecompressMemoryNV-None-07684

The [`memoryDecompression`](features.html#features-memoryDecompression) feature
**must** be enabled

Valid Usage (Implicit)

* 
[](#VUID-vkCmdDecompressMemoryNV-commandBuffer-parameter) VUID-vkCmdDecompressMemoryNV-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdDecompressMemoryNV-pDecompressMemoryRegions-parameter) VUID-vkCmdDecompressMemoryNV-pDecompressMemoryRegions-parameter

 `pDecompressMemoryRegions` **must** be a valid pointer to an array of `decompressRegionCount` valid [VkDecompressMemoryRegionNV](#VkDecompressMemoryRegionNV) structures

* 
[](#VUID-vkCmdDecompressMemoryNV-commandBuffer-recording) VUID-vkCmdDecompressMemoryNV-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdDecompressMemoryNV-commandBuffer-cmdpool) VUID-vkCmdDecompressMemoryNV-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics, or compute operations

* 
[](#VUID-vkCmdDecompressMemoryNV-renderpass) VUID-vkCmdDecompressMemoryNV-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdDecompressMemoryNV-videocoding) VUID-vkCmdDecompressMemoryNV-videocoding

 This command **must** only be called outside of a video coding scope

* 
[](#VUID-vkCmdDecompressMemoryNV-decompressRegionCount-arraylength) VUID-vkCmdDecompressMemoryNV-decompressRegionCount-arraylength

 `decompressRegionCount` **must** be greater than `0`

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Graphics

Compute
Action

The `VkDecompressMemoryRegionNV` structure is defined as:

// Provided by VK_NV_memory_decompression
typedef struct VkDecompressMemoryRegionNV {
    VkDeviceAddress                       srcAddress;
    VkDeviceAddress                       dstAddress;
    VkDeviceSize                          compressedSize;
    VkDeviceSize                          decompressedSize;
    VkMemoryDecompressionMethodFlagsNV    decompressionMethod;
} VkDecompressMemoryRegionNV;

* 
`srcAddress` is the address where compressed data is stored.

* 
`dstAddress` is the destination address where decompressed data will
be written.

* 
`compressedSize` is the size of compressed data in bytes.

* 
`decompressedSize` is the size of decompressed data in bytes.

* 
`decompressionMethod` is a bitmask of
`VkMemoryDecompressionMethodFlagBitsNV` with a single bit set
specifying the method used to decompress data.

Valid Usage

* 
[](#VUID-VkDecompressMemoryRegionNV-srcAddress-07685) VUID-VkDecompressMemoryRegionNV-srcAddress-07685

The `srcAddress` **must** be 4 byte aligned

* 
[](#VUID-VkDecompressMemoryRegionNV-srcAddress-07686) VUID-VkDecompressMemoryRegionNV-srcAddress-07686

The memory in range `srcAddress` and `srcAddress` + 
`compressedSize` **must** be valid and bound to a `VkDeviceMemory`
object

* 
[](#VUID-VkDecompressMemoryRegionNV-dstAddress-07687) VUID-VkDecompressMemoryRegionNV-dstAddress-07687

The `dstAddress` **must** be 4 byte aligned

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-09395) VUID-VkDecompressMemoryRegionNV-decompressionMethod-09395

If `decompressionMethod` is
`VK_MEMORY_DECOMPRESSION_METHOD_GDEFLATE_1_0_BIT_NV`, then
`decompressedSize` **must** be less than or equal to 65536 bytes

* 
[](#VUID-VkDecompressMemoryRegionNV-dstAddress-07688) VUID-VkDecompressMemoryRegionNV-dstAddress-07688

The memory in range `dstAddress` and `dstAddress` + 
`decompressedSize` **must** be valid and bound to a
`VkDeviceMemory` object

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressedSize-07689) VUID-VkDecompressMemoryRegionNV-decompressedSize-07689

The `decompressedSize` **must** be large enough to hold the
decompressed data based on the `decompressionMethod`

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-07690) VUID-VkDecompressMemoryRegionNV-decompressionMethod-07690

The `decompressionMethod` **must** have a single bit set

* 
[](#VUID-VkDecompressMemoryRegionNV-srcAddress-07691) VUID-VkDecompressMemoryRegionNV-srcAddress-07691

The `srcAddress` to `srcAddress` +  `compressedSize`
region **must** not overlap with the `dstAddress` and `dstAddress`
+  `decompressedSize` region

Valid Usage (Implicit)

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-parameter) VUID-VkDecompressMemoryRegionNV-decompressionMethod-parameter

 `decompressionMethod` **must** be a valid combination of [VkMemoryDecompressionMethodFlagBitsNV](#VkMemoryDecompressionMethodFlagBitsNV) values

* 
[](#VUID-VkDecompressMemoryRegionNV-decompressionMethod-requiredbitmask) VUID-VkDecompressMemoryRegionNV-decompressionMethod-requiredbitmask

 `decompressionMethod` **must** not be `0`

To decompress data between one or more memory regions by specifying
decompression parameters indirectly in a buffer, call:

// Provided by VK_NV_memory_decompression
void vkCmdDecompressMemoryIndirectCountNV(
    VkCommandBuffer                             commandBuffer,
    VkDeviceAddress                             indirectCommandsAddress,
    VkDeviceAddress                             indirectCommandsCountAddress,
    uint32_t                                    stride);

* 
`commandBuffer` is the command buffer into which the command will be
recorded.

* 
`indirectCommandsAddress` is the device address containing
decompression parameters laid out as an array of
[VkDecompressMemoryRegionNV](#VkDecompressMemoryRegionNV) structures.

* 
`indirectCommandsCountAddress` is the device address containing the
decompression count.

* 
`stride` is the byte stride between successive sets of decompression
parameters located starting from `indirectCommandsAddress`.

Each region specified in `indirectCommandsAddress` is decompressed from
the source to destination region based on the specified decompression
method.

Valid Usage

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-None-07692) VUID-vkCmdDecompressMemoryIndirectCountNV-None-07692

The [`memoryDecompression`](features.html#features-memoryDecompression) feature
**must** be enabled

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-07693) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-07693

If `indirectCommandsAddress` comes from a non-sparse buffer then it
**must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-07694) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsAddress-07694

The [VkBuffer](resources.html#VkBuffer) that `indirectCommandsAddress` comes from **must**
have been created with the `VK_BUFFER_USAGE_INDIRECT_BUFFER_BIT` bit
set

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-offset-07695) VUID-vkCmdDecompressMemoryIndirectCountNV-offset-07695

`offset` **must** be a multiple of `4`

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07696) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07696

If `indirectCommandsCountAddress` comes from a non-sparse buffer
then it **must** be bound completely and contiguously to a single
`VkDeviceMemory` object

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07697) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07697

The [VkBuffer](resources.html#VkBuffer) that `indirectCommandsCountAddress` comes from
**must** have been created with the
`VK_BUFFER_USAGE_INDIRECT_BUFFER_BIT` bit set

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07698) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07698

`indirectCommandsCountAddress` **must** be a multiple of `4`

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07699) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07699

The count stored in `indirectCommandsCountAddress` **must** be less
than or equal to
`VkPhysicalDeviceMemoryDecompressionPropertiesNV`::`maxDecompressionIndirectCount`

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-stride-07700) VUID-vkCmdDecompressMemoryIndirectCountNV-stride-07700

`stride` **must** be a multiple of `4` and **must** be greater than or
equal to sizeof(`VkDecompressMemoryRegionNV`)

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07701) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07701

If the count stored in `indirectCommandsCountAddress` is equal to
`1`, (`offset` + 
sizeof(`VkDecompressMemoryRegionNV`)) **must** be less than or equal
to the size of the [VkBuffer](resources.html#VkBuffer) that `indirectCommandsAddress`
comes from

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07702) VUID-vkCmdDecompressMemoryIndirectCountNV-indirectCommandsCountAddress-07702

If the count stored in `indirectCommandsCountAddress` is greater
than `1`, `indirectCommandsAddress` + 
sizeof(`VkDecompressMemoryRegionNV`) +  (`stride`
× (count stored in `countBuffer` - 1)) **must** be less than or
equal to the last valid address in the [VkBuffer](resources.html#VkBuffer) that
`indirectCommandsAddress` was created from

Valid Usage (Implicit)

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-parameter) VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-parameter

 `commandBuffer` **must** be a valid [VkCommandBuffer](cmdbuffers.html#VkCommandBuffer) handle

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-recording) VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-recording

 `commandBuffer` **must** be in the [recording state](cmdbuffers.html#commandbuffers-lifecycle)

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-cmdpool) VUID-vkCmdDecompressMemoryIndirectCountNV-commandBuffer-cmdpool

 The `VkCommandPool` that `commandBuffer` was allocated from **must** support graphics, or compute operations

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-renderpass) VUID-vkCmdDecompressMemoryIndirectCountNV-renderpass

 This command **must** only be called outside of a render pass instance

* 
[](#VUID-vkCmdDecompressMemoryIndirectCountNV-videocoding) VUID-vkCmdDecompressMemoryIndirectCountNV-videocoding

 This command **must** only be called outside of a video coding scope

Host Synchronization

* 
Host access to `commandBuffer` **must** be externally synchronized

* 
Host access to the `VkCommandPool` that `commandBuffer` was allocated from **must** be externally synchronized

Command Properties

[Command Buffer Levels](cmdbuffers.html#VkCommandBufferLevel)
[Render Pass Scope](renderpass.html#vkCmdBeginRenderPass)
[Video Coding Scope](videocoding.html#vkCmdBeginVideoCodingKHR)
[Supported Queue Types](devsandqueues.html#VkQueueFlagBits)
[Command Type](fundamentals.html#fundamentals-queueoperation-command-types)

Primary

Secondary
Outside
Outside
Graphics

Compute
Action

Bits which **can** be set in
`VkDecompressMemoryRegionNV`::`decompressionMethod` specifying the
decompression method to select, or returned in
`VkPhysicalDeviceMemoryDecompressionPropertiesNV`::`decompressionMethods`
specifying the available decompression methods are:

// Provided by VK_NV_memory_decompression
// Flag bits for VkMemoryDecompressionMethodFlagBitsNV
typedef VkFlags64 VkMemoryDecompressionMethodFlagBitsNV;
static const VkMemoryDecompressionMethodFlagBitsNV VK_MEMORY_DECOMPRESSION_METHOD_GDEFLATE_1_0_BIT_NV = 0x00000001ULL;

* 
`VK_MEMORY_DECOMPRESSION_METHOD_GDEFLATE_1_0_BIT_NV` specifies that
the GDeflate 1.0 algorithm is used to decompress data.

// Provided by VK_NV_memory_decompression
typedef VkFlags64 VkMemoryDecompressionMethodFlagsNV;

`VkMemoryDecompressionMethodFlagsNV` is a bitmask type for specifying a
mask of one or more `VkMemoryDecompressionMethodFlagBitsNV`:
