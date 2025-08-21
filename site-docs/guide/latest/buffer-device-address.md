# Buffer Device Address

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/buffer_device_address.html

## Table of Contents

- [Extension](#_extension)
- [Name alias](#_name_alias)
- [Vulkan Side](#_vulkan_side)
- [SPIR-V Side](#_spir_v_side)
- [Capability](#_capability)
- [Addressing Model](#_addressing_model)
- [shaderInt64](#_shaderint64)
- [Alignment](#_alignment)
- [Alignment Example](#_alignment_example)
- [Nullptr](#_nullptr)
- [Cross stage variables](#_cross_stage_variables)
- [Cross_stage_variables](#_cross_stage_variables)
- [OpTypeForwardPointer and infinite loops](#_optypeforwardpointer_and_infinite_loops)
- [OpTypeForwardPointer_and_infinite_loops](#_optypeforwardpointer_and_infinite_loops)
- [Accesses](#_accesses)
- [Overview](#_overview)

## Content

Buffer Device Address allows you to have a pointer to the `VkBuffer` in your shaders. There are many other usages such as Ray Tracing, GPU Side tooling, etc.

|  | This will be more of a technical breakdown of how it works, if you looking for a simple "how do I just use this", then please take a look at the [Vulkan Samples](https://github.com/KhronosGroup/Vulkan-Samples/tree/main/samples/extensions/buffer_device_address). |
| --- | --- |

The original proposal was done with the  `VK_EXT_buffer_device_address` extension. Shortly afterwards, `VK_KHR_buffer_device_address` was added, which had some minor feature differences. Starting in Vulkan 1.2 this has become core and it is very widely available on GPUs on every platform. Starting in Vulkan 1.3 it became required, so if you are using Vulkan 1.3, you are guaranteed support.

The naming of this `Buffer Device Address` feature will be different depending on where you look.

For GLSL, it is `buffer reference` (see [GL_EXT_buffer_reference](https://github.com/KhronosGroup/GLSL/blob/main/extensions/ext/GLSL_EXT_buffer_reference.txt)). This is because syntactically it’s used more like a C++ reference than a pointer.

For SPIR-V, it is `PhysicalStorageBuffer` (see [SPV_KHR_physical_storage_buffer](https://htmlpreview.github.io/?https://github.com/KhronosGroup/SPIRV-Registry/blob/main/extensions/KHR/SPV_KHR_physical_storage_buffer.html)). The name comes from the fact there was a `StorageBuffer` and now it is "Physical". (`Physical` is from "physical addressing" which is a concept in `Kernel` SPIR-V)

If you are coming from DirectX, you will know the feature as `GPU virtual address`.

From the Vulkan code, the only 3 things you need to do is

Enable the `bufferDeviceAddress` feature. (Also the extension if using Vulkan 1.0 or 1.1)

Add `VK_BUFFER_USAGE_SHADER_DEVICE_ADDRESS_BIT_KHR` when creating your `VkBuffer`.

Add `VK_MEMORY_ALLOCATE_DEVICE_ADDRESS_BIT_KHR` when allocating your `VkDeviceMemory`.

From here you can use the `vkGetBufferDeviceAddress` call and it will return a `VkDeviceAddress`. This is now your 64-bit pointer to that `VkBuffer` that can be handed down into your shader.

|  | For tools, the `vkGetBufferDeviceAddress` function might break assumptions that Vulkan function only return `void` or `VkResult` |
| --- | --- |

|  | If you are using GLSL/HLSL/Slang/etc then the following is all taken care for you! |
| --- | --- |

The SPIR-V will contain the `OpCapability PhysicalStorageBufferAddresses` instruction that will match up with `VkPhysicalDeviceVulkan12Features::bufferDeviceAddress` (or `VkPhysicalDeviceBufferDeviceAddressFeatures::bufferDeviceAddress`) to let everyone know the device does support this.

SPIR-V has an [Addressing Model](https://registry.khronos.org/SPIR-V/specs/unified1/SPIRV.html#Addressing_Model) that has 3 group of options

`Logical` - this is what Vulkan 1.0 uses, it has no concept of pointers

`Physical32`/`Physical64` - this for OpenCL

`PhysicalStorageBuffer64` - this is what you will use if you are making use of Buffer Device Address

Since these `VkDeviceAddress` are represented as 64-bit integer pointers in your shader, you will likely want `shaderInt64` support for your device.

Some device migth support `bufferDeviceAddress`, but not `shaderInt64`. The way around this situation is to make everything an `uvec2` (see [GL_EXT_buffer_reference_uvec2](https://github.com/KhronosGroup/GLSL/blob/main/extensions/ext/GLSL_EXT_buffer_reference_uvec2.txt)).

All variables accessed with `PhysicalStorageBuffer` must have an `Aligned` memory operand to it.

%x = OpLoad %type %ptr Aligned 16
OpStore %ptr %obj Aligned 16

Shading languages will have a default, but can allow you to align it explicitly (ex `buffer_reference_alignment`).

The goal of this alignment is this is a promise for how aligned this specific pointer is.
The compiler has no idea what the address will be when the shader is compiled.
By providing an alignment it can generate valid code to match the requirement.
The user is responsible to confirm the address they use is aligned to it.

layout(buffer_reference, buffer_reference_align = 64) buffer MyBDA {
    uint data;
};

MyBDA ptr_a; // at 0x1000
MyBDA ptr_b; // at 0x1010
MyBDA ptr_c; // at 0x1040

ptr_a.data = 0; // (Aligned 64) valid!
ptr_b.data = 0; // (Aligned 64) invalid!
ptr_c.data = 0; // (Aligned 64) valid!

When deciding on an alignment, the minimum value will always be the size greater than or equal to the largest scalar/component type in the block.

// alignment must be at least 4
layout(buffer_reference) buffer MyBDA {
    vec4 a; // scalar is float
};

// alignment must be at least 1
layout(buffer_reference) buffer MyBDA {
    uint8_t a; // scalar is 8-bit int
};

// alignment must be at least 8
layout(buffer_reference) buffer MyBDA {
    uint a; // 32-bit
    double b; // 64-bit
};

To help explain alignment, lets take an example of loading an array of vectors

layout(buffer_reference, buffer_reference_align = ???) buffer MyBDA {
    uvec4 data[];
};

MyBDA ptr; // at 0x1000
ptr.data[i] = uvec4(0);

Here we have 2 options, we could set the `Aligned` to be `4` or `16`.

If we set alignment to `16` we are letting the compiler know it can load 16 bytes at a time, so it will hopefully do a vector load/store on the memory.

If we set alignment to `4` the compiler will likely have no way to infer the real alignment and will now do 4 scalar int load/store on the memory.

|  | Some GPUs can do vector load/store even on unaligned addresses. |
| --- | --- |

For the next case, if we had `uvec3` instead of `uvec4` such as

layout(buffer_reference, buffer_reference_align = 4, scalar) buffer MyBDA {
    uvec3 data[];
};

data[0]; // 0x1000
data[1]; // 0x100C
data[2]; // 0x1018
data[3]; // 0x1024

We know that setting the alignment to `16` would be violated at `data[1]` and therefore we need to use an alignment of `4` in this case.
Luckily shading languages will help do this for you as seen in both [glslang](https://godbolt.org/z/jWGKax1ed) and [slang](https://godbolt.org/z/Y7xW3Mfd4) .

SPIR-V has a `OpConstantNull`, but that can’t be used with `PhysicalStorageBuffer`. The way around this is to either convert the pointer to an integer with `OpConvertPtrToU` or to a `uvec2` with `OpBitcast`.

Vulkan defines the integer value of `0` to be null (as everyone would hopefully expect!).

There is still on-going discussion to clarify if/how passing pointers from two stages works (ex. vertex to fragment).

The main issue is you may get validation layers errors with the `Location` matching (see [https://github.com/KhronosGroup/Vulkan-ValidationLayers/pull/5349](https://github.com/KhronosGroup/Vulkan-ValidationLayers/pull/5349)).

The suggestion is to just pass a `uvec2` or `int64` across stages and re-cast it in your consumer stage.

The `OpTypeForwardPointer` is used to forward reference the type of the pointer. This is useful if the app wants to do something like a linked-list

layout(buffer_reference) buffer Node;

layout(buffer_reference, std430) buffer Node {
    Node next_node;
    int payload;
};

layout(set = 0, binding = 0, std430) buffer SSBO {
    Node start;
};

You will see the following SPIR-V

            OpTypeForwardPointer %Node_ptr PhysicalStorageBuffer
    %SSBO = OpTypeStruct %Node_ptr
     %int = OpTypeInt 32 1
    %Node = OpTypeStruct %Node_ptr %int
%Node_ptr = OpTypePointer PhysicalStorageBuffer %Node
%SSBO_ptr = OpTypePointer StorageBuffer %SSBO
     %var = OpVariable %SSBO_ptr StorageBuffer

When parsing this SPIR-V to do reflection, it is very easy to get into an infinite loop, so be careful.

|  | If you want some SPIR-V to test this, look at the `buffer_handle_*.spv` tests in [SPIR-V Reflect Tests](https://github.com/KhronosGroup/SPIRV-Reflect/blob/main/tests/glsl). |
| --- | --- |

If you take the following simple GLSL example

#version 450
#extension GL_EXT_buffer_reference : enable

layout(buffer_reference) buffer BDA {
    int a;
};

layout(set=0, binding=0) uniform InData {
    BDA b;
};

void main() {
    b.a = 0;
}

You will see the following SPIR-V

%bda_ptr = OpTypePointer PhysicalStorageBuffer %bda_struct
%ubo_ptr = OpTypePointer Uniform %bda_ptr
%int_ptr = OpTypePointer PhysicalStorageBuffer %type_int

 %1 = OpAccessChain %ubo_ptr %3 %int_0
 %2 = OpLoad %bda_ptr %1
 %3 = OpAccessChain %int_ptr %2 %int_0
      OpStore %3 %int_0 Aligned 16

It is easy to think that this `OpLoad` here is dereferencing the pointer before we store into it.

This assumption is wrong, and instead the `OpLoad` is loading the logical pointer from the `ubo`. The access chain is computing an offset from that to the physical pointer. From here, the `OpStore` access the right location in memory through the pointer.

Therefore in the above example, there is only a write access to that memory.

The following diagram tries to capture visually how Buffer Device Address works

![buffer_device_address_overview.png](_images/buffer_device_address_overview.png)
