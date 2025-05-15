# Vulkan Samples

## Metadata

- **Component**: samples
- **Version**: latest
- **URL**: /samples/latest/README.html

## Table of Contents

- [Introduction](#_introduction)
- [Goals](#_goals)
- [Samples](#_samples)
- [General information](#_general_information)
- [Setup](#_setup)
- [Build](#_build)
- [Supported Platforms](#_supported_platforms)
- [Usage](#_usage)
- [License](#_license)
- [Trademarks](#_trademarks)
- [Contributions](#_contributions)
- [Related resources](#_related_resources)

## Content

The Vulkan Samples is collection of resources to help you develop optimized Vulkan applications. If you are new to Vulkan the API samples are the right place to start. Additionally you may find the following links useful: Vulkan Guide Get Started in Vulkan Performance samples show the recommended best practice together with real-time profiling information. They are more advanced but also contain a detailed tutorial with more in-detail explanations. Create a collection of resources that demonstrate best-practice recommendations in Vulkan Create tutorials that explain the implementation of best-practices and include performance analysis guides Create a framework that can be used as reference material and also as a sandbox for advanced experimentation with Vulkan Listing of all samples available in this repository Project Basics Controls Debug window Create a Sample Vulkan Essentials How does Vulkan compare to OpenGL ES? What should you expect when targeting Vulkan? Misc Driver version Memory limits Prerequisites: git with git large file storage (git-lfs). Clone the repo with submodules using the following command: git clone --recurse-submodules https://github.com/KhronosGroup/Vulkan-Samples.git cd Vulkan-Samples Follow build instructions for your platform below. The full repository is very large, and some ISPs appear to have trouble providing a robust connection to github while the clone is being made. If you notice problems such as submodules downloading at reported rates in the tens of kB/s, or fatal timeout errors occurring, these may be due to network routing issues to github within your ISP’s internal network, rather than anything wrong in your own networking setup. It can be very difficult to get ISPs to acknowledge such problems exist, much less to fix them. One workaround is to switch the repository to use ssh protocol prior to the submodule download, which can be done via e.g. git clone git@github.com:KhronosGroup/Vulkan-Samples.git cd Vulkan-Samples perl -i -p -e 's|https://(.*?)/|git@\1:|g' .gitmodules git submodule sync git submodule update While this can be a good alternative if you are running into this connection issue, you must have GitHub ssh key authentication setup to use ssh protocol - see Connecting to GitHub with SSH for details. So it is a not a solution we can implement as the repository default. Another option which may help is to run github through a VPN service. Windows - Build Guide Linux - Build Guide Android - Build Guide macOS - Build Guide iOS - Build Guide The following shows some example command line usage on how to configure and run the Vulkan Samples. Make sure that you are running the samples from the root directory of the repository. Otherwise the samples will not be able to find the assets. ./build/app/bin///vulkan_samples # For the entire usage use vulkan_samples --help # For subcommand usage use vulkan_samples --help # Run Swapchain Images sample vulkan_samples sample swapchain_images # Run AFBC sample in benchmark mode for 5000 frames vulkan_samples sample afbc --benchmark --stop-after-frame 5000 # Run compute nbody using headless_surface and take a screenshot of frame 5 # Note: headless_surface uses VK_EXT_headless_surface. # This will create a surface and a Swapchain, but present will be a no op. # The extension is supported by Swiftshader(https://github.com/google/swiftshader). # It allows to quickly test content in environments without a GPU. vulkan_samples sample compute_nbody --headless_surface -screenshot 5 # Run all the performance samples for 10 seconds in each configuration vulkan_samples batch --category performance --duration 10 # Run Swapchain Images sample on an Android device adb shell am start-activity -n com.khronos.vulkan_samples/com.khronos.vulkan_samples.SampleLauncherActivity -e sample swapchain_images See LICENSE. This project has several third-party dependencies This project uses assets from vulkan-samples-assets. Each one has its own license. Vulkan is a registered trademark of the Khronos Group Inc. Donated to Khronos by Arm, with further contributions by Sascha Willems and Adam Sawicki. See CONTRIBUTORS for the full contributor list. Also see CONTRIBUTING for contribution guidelines. Mali GPU Best Practices: A document with recommendations for efficient API usage
