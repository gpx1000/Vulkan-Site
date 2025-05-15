# What is SPIR-V

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/what_is_spirv.html

## Table of Contents

- [SPIR-V Interface and Capabilities](#_spir_v_interface_and_capabilities)
- [SPIR-V_Interface_and_Capabilities](#_spir_v_interface_and_capabilities)
- [Compilers](#_compilers)
- [glslang](#_glslang)
- [Shaderc](#_shaderc)
- [DXC](#_dxc)
- [Clspv](#_clspv)
- [Tools and Ecosystem](#_tools_and_ecosystem)
- [Tools_and_Ecosystem](#_tools_and_ecosystem)
- [SPIRV-Tools](#_spirv_tools)
- [SPIRV-Cross](#_spirv_cross)
- [SPIRV-LLVM](#_spirv_llvm)

## Content

Please read the SPIRV-Guide for more in detail information about SPIR-V SPIR-V is a binary intermediate representation for graphical-shader stages and compute kernels. With Vulkan, an application can still write their shaders in a high-level shading language such as GLSL or HLSL, but a SPIR-V binary is needed when using vkCreateShaderModule. Khronos has a very nice white paper about SPIR-V and its advantages, and a high-level description of the representation. There are also two great Khronos presentations from Vulkan DevDay 2016 here and here (video of both). Vulkan has an entire section that defines how Vulkan interfaces with SPIR-V shaders. Most valid usages of interfacing with SPIR-V occur during pipeline creation when shaders are compiled together. SPIR-V has many capabilities as it has other targets than just Vulkan. To see the supported capabilities Vulkan requires, one can reference the Appendix. Some extensions and features in Vulkan are just designed to check if some SPIR-V capabilities are supported or not. glslang is the Khronos reference front-end for GLSL, HLSL and ESSL, and sample SPIR-V generator. There is a standalone glslangValidator tool that is included that can be used to create SPIR-V from GLSL, HLSL and ESSL. A collection of tools, libraries, and tests for Vulkan shader compilation hosted by Google. It contains glslc which wraps around core functionality in glslang and SPIRV-Tools. Shaderc also contains spvc which wraps around core functionality in SPIRV-Cross and SPIRV-Tools. Shaderc builds both tools as a standalone command line tool (glslc) as well as a library to link to (libshaderc). DirectXShaderCompiler also supports translating HLSL into the SPIR-V. Clspv is a prototype compiler for a subset of OpenCL C to SPIR-V to be used as Vulkan compute shaders. There is a rich ecosystem of tools to take advantage of SPIR-V. The Vulkan SDK gives an overview of all the SPIR-V tools that are built and packaged for developers. The Khronos SPIRV-Tools project provides C and C++ APIs and a command line interface to work with SPIR-V modules. More information in the SPIRV-Guide. The Khronos SPIRV-Cross project is a practical tool and library for performing reflection on SPIR-V and disassembling SPIR-V back to a desired high-level shading language. For more details, Hans Kristian, the main developer of SPIR-V Cross, has given two great presentations about what it takes to create a tool such as SPIR-V Cross from 2018 Vulkanised (video) and 2019 Vulkanised (video) The Khronos SPIRV-LLVM project is a LLVM framework with SPIR-V support. It’s intended to contain a bi-directional converter between LLVM and SPIR-V. It also serves as a foundation for LLVM-based front-end compilers targeting SPIR-V.
