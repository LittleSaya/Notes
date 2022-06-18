| Semaphore | Fence |
| --- | --- |
| 有`signaled`和`unsignaled`两种状态 | 有`signaled`和`unsignaled`两种状态 |
| 用于同步GPU上的工作负载 | 用于在CPU和GPU之间同步工作负载 |
| 使用完成后自动转变为`unsignaled`状态 | 使用完成后需要手动将状态改为`unsignaled` |
| 不会阻塞CPU | 会阻塞CPU |

基本上有两个地方需要使用同步原语：
1. SwapChain。由于与SwapChain相关的操作都是在GPU上执行的，因此我们使用semaphore，不阻塞CPU。
2. 等待上一帧绘制结束。我们不希望同时绘制很多帧，因此在上一帧绘制完成之前，CPU需要等待。
