# Shaders

## Metadata

- **Component**: samples
- **Version**: latest
- **URL**: /samples/latest/shaders/README.html

## Table of Contents

- [Shader languages](#_shader_languages)
- [Compiling shaders](#_compiling_shaders)
- [Further information](#_further_information)

## Content

This folder contains the textual shaders for the samples. All samples come with GLSL shaders and some optionally with HLSL shaders. For samples that support both shader language this is a good way to compare GLSL to HLSL syntax when targeting SPIR-V for Vulkan.

The samples load offline compiled SPIR-V variants of the GLSL/HLSL shaders. If you have the appropriate compiler installed, e.g. via the LunarG VUlkan SDK, shaders will be automatically compiled when building the samples project.

The [Vulkan Guide](../../../guide/latest/index.html) contains further information on how to use HLSL with Vulkan and how it compares to GLSL:

* 
[HLSL in Vulkan](../../../guide/latest/hlsl.html)

* 
[High level shading language comparison](../../../guide/latest/high_level_shader_language_comparison.html)
