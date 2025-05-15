# Synchronization

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/synchronization.html

## Table of Contents

- [Validation](#_validation)
- [Pipeline Barriers](#_pipeline_barriers)
- [VK_KHR_synchronization2](#_vk_khr_synchronization2)

## Content

Synchronization is one of the most powerful but also most complex parts of using Vulkan. The application developer is now responsible for managing synchronization using the various Vulkan synchronization primitives. Improper use of synchronization can lead to hard-to-find bugs as well as poor performance in cases where the the GPU is unnecessarily idle. There are a set of examples and a Understanding Vulkan Synchronization blog provided by Khronos on how to use some of the synchronization primitives. There are also presentations from Tobias Hector from past Vulkan talks: part 1 slides (video) and part 2 slides (video). The following is an overview diagram of the difference between VkEvent, VkFence, and VkSemaphore The Khronos Validation Layer has implemented some validation for synchronization. It can easily be enabled by the Vulkan Configurator included with the Vulkan SDK. A detailed whitepaper discussing the synchronization validation has been written as well and released as a Khronos Blog. Pipeline Barriers give control over which pipeline stages need to wait on previous pipeline stages when a command buffer is executed. While Pipeline Barriers might be hard to understand at first, there are many great Khronos talks and other resources that go more in depth on the topic. Vulkanised 2018 - Low-level mysteries of pipeline barriers (video) Vulkanised 2019 - Live Long and Optimise (video) Pipeline Analysis starting slide 12 Vulkan barriers explained blog post Yet another blog post explaining Vulkan synchronization The VK_KHR_synchronization2 extension overhauls the original core synchronization APIs to reduce complexity for application developers, as well as adding a few additional features not present in the original APIs. Read the VK_KHR_synchronization2 chapter for more info about the difference in the synchronization APIs and how to port over to using the new extension
