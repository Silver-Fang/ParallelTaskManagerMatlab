# ParallelTaskManagerMatlab

[![View 并行 任务 管理 Parallel Task Manager on File Exchange](https://www.mathworks.com/matlabcentral/images/matlab-file-exchange.svg)](https://ww2.mathworks.cn/matlabcentral/fileexchange/84978-parallel-task-manager)

MATLAB并行任务优化管理器，只需输入具体的工作函数和数据，就能自动实现高效率的并行化处理。你也可以只生成分配方案然后自行调度。

## AllocateTasksFairly

将多个任务分配到多个并行进程时，为了最大化工作效率，通常希望每个进程被赋予相当的任务量，避免某些进程过早完成任务然后空等待。同时，将单个任务拆分往往会造成一定的性能损失，在负载均衡的前提下应当尽量将单个任务交给单个进程执行。
本拆分函数接受多个任务各自的尺寸，和并行进程数目作为参数，给出合理化的任务分配方案。
对于单个较大的任务，将其拆分给多个进程执行；对于多个较小的任务，将它们合并给一个进程执行。同时为了尽量减少任务拆分，若一个大任务被决定拆分，则分到该任务的所有进程将专心执行该任务，不会被分配到其它任务；反过来，若一个进程被分配到了多个任务，则这些任务将完全由该进程独立执行，而不会再拆分给其它进程。

## TaskSplitParallelRun

本函数能够对批处理任务进行多线程调度，追求负载均衡。可以将单个大任务拆分到多个进程执行，多个小任务合并到一个进程执行，实现性能优化。由于本函数内部使用了parfeval，因此只能在主进程中运行，不能将本函数交给并行池进程调用。
