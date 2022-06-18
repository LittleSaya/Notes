| Semaphore | Fence |
| --- | --- |
| 有`signaled`和`unsignaled`两种状态 | 有`signaled`和`unsignaled`两种状态 |
| 用于同步GPU上的工作负载 | 用于在CPU和GPU之间同步工作负载 |
| 使用完成后自动转变为`unsignaled`状态 | 使用完成后需要手动将状态改为`unsignaled` |
