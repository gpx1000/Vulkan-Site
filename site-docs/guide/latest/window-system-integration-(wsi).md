# Window System Integration (WSI)

## Metadata

- **Component**: guide
- **Version**: latest
- **URL**: /guide/latest/wsi.html

## Table of Contents

- [Surface](#_surface)
- [Swapchain](#_swapchain)
- [Pre-Rotation](#_pre_rotation)

## Content

Since the Vulkan API can be used without displaying results, WSI is provided through the use of optional Vulkan extensions. Most implementations will include WSI support. The WSI design was created to abstract each platform’s windowing mechanism from the core Vulkan API. The VkSurfaceKHR object is platform agnostic and designed so the rest of the Vulkan API can use it for all WSI operations. It is enabled using the VK_KHR_surface extension. Each platform that supports a Vulkan Surface has its own way to create a VkSurfaceKHR object from its respective platform-specific API. Android - vkCreateAndroidSurfaceKHR DirectFB - vkCreateDirectFBSurfaceEXT Fuchsia - vkCreateImagePipeSurfaceFUCHSIA iOS - vkCreateIOSSurfaceMVK macOS - vkCreateMacOSSurfaceMVK Metal - vkCreateMetalSurfaceEXT VI - vkCreateViSurfaceNN Wayland - vkWaylandSurfaceCreateInfoKHR QNX - vkCreateScreenSurfaceQNX Windows - vkCreateWin32SurfaceKHR XCB - vkCreateXcbSurfaceKHR Xlib - vkCreateXlibSurfaceKHR Direct-to-Display - vkCreateDisplayPlaneSurfaceKHR Once a VkSurfaceKHR is created there are various capabilities, formats, and presentation modes to query for. The VkSwapchainKHR object provides the ability to present rendering results to a surface through an array of VkImage objects. The swapchain’s various present modes determine how the presentation engine is implemented. Khronos' sample and tutorial explain different considerations to make when creating a swapchain and selecting a presentation mode. Mobile devices can be rotated, therefore the logical orientation of the application window and the physical orientation of the display may not match. Applications need to be able to operate in two modes: portrait and landscape. The difference between these two modes can be simplified to just a change in resolution. However, some display subsystems always work on the “native” (or “physical”) orientation of the display panel. Since the device has been rotated, to achieve the desired effect the application output must also rotate. In order for your application to get the most out of Vulkan on mobile platforms, such as Android, implementing pre-rotation is a must. There is a detailed blog post from Google that goes over how to handle the surface rotation by specifying the orientation during swapchain creation and also comes with a standalone example. The Vulkan-Samples also has both a great write up of why pre-rotation is a problem as well as a sample to run that shows a way to solve it in the shader. If using an Adreno GPU powered device, Qualcomm suggests making use of the VK_QCOM_render_pass_transform extension to implement pre-rotation.
