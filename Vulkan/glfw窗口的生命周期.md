- 创建窗口之前，初始化glfw
  - `glfwInit()`
  - `glfwWindowHint() // 设置窗口属性，如能否调整大小`
  - `glfwWindowHint()`
  - `glfwWindowHint()`
  - ...
- 创建窗口
  - `glfwCreateWindow(int width, int height, const char* title, GLFWmonitor* monitor, GLFWwindow* share)`
    - 参数`width`：窗口宽度
    - 参数`height`：窗口高度
    - 参数`title`：窗口标题
    - 参数`monitor`：指定显示器
    - 参数`share`：与OpenGL相关的参数
- 主循环
  ```c
  while (!glfwWindowShouldClose(window)) {
      glfwPollEvents();
  }
  ```
- 程序结束
  - `glfwDestroyWindow(window)`
  - `glfwTerminate()`
