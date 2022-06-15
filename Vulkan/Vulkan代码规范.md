1. 所有的Vulkan函数、枚举和结构体都定义在头文件`vulkan.h`中
2. 函数以`vk`开头
3. 枚举类型和结构体以`Vk`开头
4. 枚举值以`VK_`开头

基本上所有API都使用结构体给函数提供实参，对象通常用如下方式创建：

```c
VkXXXCreateInfo createInfo{};
createInfo.sType = VK_STRUCTURE_TYPE_XXX_CREATE_INFO;
createInfo.pNext = nullptr;
createInfo.foo = ...;
createInfo.bar = ...;

VkXXX object;
if (vkCreateXXX(&createInfo, nullptr, &object) != VK_SUCCESS) {
    std::cerr << "failed to create object" << std::endl;
    return false;
}
```
5. Vulkan的许多结构体需要通过`sType`成员显式指定其类型
6. 成员`pNext`可用于指向扩展结构体
7. 创建或销毁对象的函数有一个叫`VkAllocationCallbacks`的参数，可以使用该参数自定义驱动内存的分配
8. 几乎所有函数都会返回一个`VkResult`值，这个值要么是`VK_SUCCESS`，要么是一个错误码
