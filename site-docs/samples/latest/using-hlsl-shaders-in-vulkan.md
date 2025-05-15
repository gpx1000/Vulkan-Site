# Using HLSL shaders in Vulkan

## Metadata

- **Component**: samples
- **Version**: latest
- **URL**: /samples/latest/samples/api/hlsl_shaders/README.html

## Table of Contents

- [HLSL Syntax](#_hlsl_syntax)
- [Glslang](#_glslang)
- [Converting HLSL to SPIR-V](#_converting_hlsl_to_spir_v)
- [Converting_HLSL_to_SPIR-V](#_converting_hlsl_to_spir_v)
- [Creating the shader module](#_creating_the_shader_module)
- [Creating_the_shader_module](#_creating_the_shader_module)

## Content

The source for this sample can be found in the Khronos Vulkan samples github repository. This tutorial, along with the accompanying example code, shows how to use shaders written in the High Level Shading Language (HLSL) in Vulkan at runtime. Vulkan does not directly consume shaders in a human-readable text format, but instead uses SPIR-V as an intermediate representation. This opens the option to use shader languages other than e.g. GLSL, as long as they can target the Vulkan SPIR-V environment. One such language is Microsoft’s HLSL, which is the shading language for DirectX. Details on how HLSL fits into the Vulkan ecosystem can be found in this Vulkan guide chapter. HLSL is a bit more object-oriented than GLSL, but the general structure of a shader is similar Vulkan-specific functions are marked with the implicit vk namespace: struct VSInput { [[vk::location(0)]] float3 Pos : POSITION0; [[vk::location(1)]] float2 UV : TEXCOORD0; [[vk::location(2)]] float3 Normal : NORMAL0; }; struct UBO { float4x4 projection; float4x4 model; float4 viewPos; }; cbuffer ubo : register(b0, space0) { UBO ubo; } struct VSOutput { float4 Pos : SV_POSITION; [[vk::location(0)]] float2 UV : TEXCOORD0; }; VSOutput main(VSInput input) { VSOutput output = (VSOutput)0; output.UV = input.UV; output.Pos = mul(ubo.projection, mul(ubo.model, float4(input.Pos.xyz, 1.0))); return output; } The Vulkan samples use Glslang for converting shaders to SPIR-V at runtime. Glslang is the reference GLSL validator and translator, but also supports HLSL as an input language. HLSL support in Glslang limited though and for a more feature complete HLSL to SPIR-V compiler, you can also use the DirectX shader compiler. For the basic shader in this tutorial, we can go with Glslang though, as it supports all features we require. Loading HLSL with Glslang is similar to loading GLSL, but requires different parameters. Here are the relevant parts that differ from loading HLSL from the HlslShaders::load_hlsl_shader function of the sample: std::vector spirv; // Use HLSL parsing rules and semantics (EShMsgReadHlsl) EShMessages messages = static_cast(EShMsgReadHlsl | ...); ... // Language needs to be selected based on the shader stage EShLanguage language = EShLangVertex; glslang::TShader shader(language); ... // Set the source language to HLSL shader.setEnvInput(glslang::EShSourceHlsl, language, glslang::EShClientVulkan, 1); ... // Parse the HLSL input if (!shader.parse(&glslang::DefaultTBuiltInResource, 100, false, messages)) { ... } // Add shader to new program object. glslang::TProgram program; program.addShader(&shader); // Link program. if (!program.link(messages)) { ... } ... // Translate to SPIRV glslang::TIntermediate *intermediate = program.getIntermediate(language); ... glslang::GlslangToSpv(*intermediate, spirv, &logger); ... The call to glslang::GlslangToSpv will generate the SPIR-V bytecode that we can use to create the Vulkan shader module from: VkShaderModule shader_module; VkShaderModuleCreateInfo module_create_info{}; module_create_info.sType = VK_STRUCTURE_TYPE_SHADER_MODULE_CREATE_INFO; module_create_info.codeSize = spirv.size() * sizeof(uint32_t); module_create_info.pCode = spirv.data(); VK_CHECK(vkCreateShaderModule(get_device().get_handle(), &module_create_info, NULL, &shader_module));
