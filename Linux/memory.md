###Linux通过slab容器分配task_struct结构，这样能达到对象复用和缓存着色的目的”
* 
task_struct：学过操作系统的知道，每个进程都有一个PCB（process control block），是控制进程的唯一也是最有效的手段；在调用fork()函数创建新的进程时时系统自动为我们创建的。3.
* 
slab分配器：某些对象由于内存频繁的申请和释放，那么很可能就出现很多的碎片；