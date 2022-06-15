# What it takes to draw a triangle

1. create `VkInstance` (application description & API extensions)
2. query & select `VkPhysicalDevice`
3. create logic device `VkDevice` (`VkPhysicalDeviceFeatures` & queue families)
  > *Note: Most operations performed with Vulkan, like draw commands and memory operations, are asynchronously executed by submitting them to a `VkQueue`*
4. create `VkSurfaceKHR` (window surface, a cross-platform abstraction over windows to render to) & and `VkSwapchainKHR` (swap chain, a collection of render targets)
  > *Note: `KHR` postfix means these objects are part of a Vulkan extension*
5. create `VkImageView` (references a specific part of an image to be used) & `VkFramebuffer` (references image views that are to be used for color, depth and stencil targets)
6. Render passes (the type of images that are used during rendering operations)
7. create `VkPipeline` (describes the configurable state of the graphics card, like the viewport size and depth buffer operation and the programmable state using `VkShaderModule` objects)
  > *Note: One of the most distinctive features of Vulkan compared to existing APIs, is that almost all configuration of the graphics pipeline needs to be set in advance. That means that if you want to switch to a different shader or slightly change your vertex layout, then you need to entirely recreate the graphics pipeline. That means that you will have to create many VkPipeline objects in advance for all the different combinations you need for your rendering operations. Only some basic configuration, like viewport size and clear color, can be changed dynamically. All of the state also needs to be described explicitly, there is no default color blend state, for example.*
8. create `VkCommandPool` associated with a specific queue family, allocate `VkCommandBuffer` from `VkCommandPool`, record operations into `VkCommandBuffer`
  > *Note: To draw a simple triangle, we need to record a command buffer with the following operations:*
  > - *Begin the render pass*
  > - *Bind the graphics pipeline*
  > - *Draw 3 vertices*
  > - *End the render pass*
9. Main loop
  - acquire image from swap chain with `vkAcquireNextImageKHR`
  - select appropriate command buffer for that image and execute it with `vkQueueSubmit`
  - return the image to the swap chain for presentation to the screen with `vkQueuePresentKHR`
  > *Note: Operations that are submitted to queues are executed asynchronously. Therefore we have to use synchronization objects like semaphores to ensure a correct order of execution.*

# Summary

- Create a VkInstance
- Select a supported graphics card (VkPhysicalDevice)
- Create a VkDevice and VkQueue for drawing and presentation
- Create a window, window surface and swap chain
- Wrap the swap chain images into VkImageView
- Create a render pass that specifies the render targets and usage
- Create framebuffers for the render pass
- Set up the graphics pipeline
- Allocate and record a command buffer with the draw commands for every possible swap chain image
- Draw frames by acquiring images, submitting the right draw command buffer and returning the images back to the swap chain