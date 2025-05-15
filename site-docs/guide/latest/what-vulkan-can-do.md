# What Vulkan Can Do

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/what_vulkan_can_do.html

## Table of Contents

- [Graphics](#_graphics)
- [Compute](#_compute)
- [Ray Tracing](#_ray_tracing)
- [Video](#_video)
- [Machine Learning](#_machine_learning)
- [Safety Critical](#_safety_critical)

## Content

Vulkan can be used to develop applications for many use cases. While Vulkan applications can choose to use a subset of the functionality described below, it was designed so a developer could use all of them in a single API. It is important to understand Vulkan is a box of tools and there are multiple ways of doing a task. 2D and 3D graphics are primarily what the Vulkan API is designed for. Vulkan is designed to allow developers to create hardware accelerated graphical applications. All Vulkan implementations are required to support Graphics, but the WSI system is not required. Due to the parallel nature of GPUs, a new style of programming referred to as GPGPU can be used to exploit a GPU for computational tasks. Vulkan supports compute variations of VkQueues, VkPipelines, and more which allow Vulkan to be used for general computation. All Vulkan implementations are required to support Compute. Ray tracing is an alternative rendering technique, based around the concept of simulating the physical behavior of light. Cross-vendor API support for ray tracing was added to Vulkan as a set of extensions in the 1.2.162 specification. These are primarily VK_KHR_ray_tracing_pipeline, VK_KHR_ray_query, and VK_KHR_acceleration_structure. There is also an older NVIDIA vendor extension exposing an implementation of ray tracing on Vulkan. This extension preceded the cross-vendor extensions. For new development, applications are recommended to prefer the more recent KHR extensions. With the Vulkan Video extensions developers can use hardware accelerated video decoding functionality in realtime. The functionality is exposed through the VK_KHR_video_queue, VK_KHR_video_decode_queue, VK_KHR_video_decode_h264 and VK_KHR_video_decode_h265 extensions. Vulkan Video adheres to the Vulkan philosophy of providing flexible, fine-grained control over video processing scheduling, synchronization, and memory utilization to the application. Provisional extensions for encoding videos are already in the works, feedback is welcome Currently, the Vulkan Working Group is looking into how to make Vulkan a first class API for exposing ML compute capabilities of modern GPUs. More information was announced at Siggraph 2019. As of now, there exists no public Vulkan API for machine learning. Vulkan SC ("Safety Critical") aims to bring the graphics and compute capabilities of modern GPUs to safety-critical systems in the automotive, avionics, industrial and medical space. It was publicly launched on March 1st 2022 and the specification is available here. Vulkan SC is based on Vulkan 1.2, but removed functionality that is not needed for safety-critical markets, increases the robustness of the specification by eliminating ignored parameters and undefined behaviors, and enables enhanced detection, reporting, and correction of run-time faults.
