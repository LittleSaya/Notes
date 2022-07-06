# VkAttachmentDescription、VkAttachmentReference、VkSubpassDescription、VkSubpassDependency和VkRenderPass之间的关系.md

一个 VkRenderPass 可以有多个 Attachment （由 VkAttachmentDescription 描述），其中每个 Attachment 可以是 Color Attachment 或者是 Depth Attachment 。

一个 VkRenderPass 可以有多个 sub-pass （由 VkSubpassDescription 描述），每个 sub-pass 可以包含多个 VkAttachmentReference ，每个 VkAttachmentReference 都引用了 VkRenderPass 的所有 Attachment 中的一个（通过成员 attachment 即被引用 attachment 的位置索引，和成员 layout 即被引用 attachment 的 layout 来引用 attachment ）。

也就是说， Attachment 是属于 render pass 的，一个 render pass 下的所有 sub-pass 都通过引用来共用自己所属的 render pass 的 Attachment 。

一个 VkRenderPass 还包括一个或多个 VkSubpassDependency ，其定义了该 render pass 下所有 sub-pass 之间的依赖关系。
