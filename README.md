## Features:
### 1.Ultra-micro real-time operating system kernel:
1)Kernel size < 10k
2)Context switch time < 8us
3)Interrupt response time < 36us
### 2.Complies with OSEK OS, OSEK COM, OSEK OIL standards:
  1)OSEK standard-compliant API
  2)OSEK standard-compliant system development process
  3)OSEK standard-compliant external communication mechanisms
### 3.Supports multiple scheduling mechanisms:
1)Preemptive scheduling
2)Non-preemptive scheduling
3)Hybrid scheduling
4.Supports static configuration
5.Supports various mainstream embedded processors


    | task                                                                 | 状态类型/函数名                       | 任务类型（TaskType） | 参数及描述     |  
| -------------------------------------------------------------------- | ------------------------------------ | -------------------- | -------------------------------------------------------------- |  
| ActivateTask（激活任务）                                             | ActivateTask（激活任务）              | TaskID（任务ID）     | 激活处于暂停状态的任务，并将其放入待执行队列中。在满足用户定义的调度策略的情况下执行任务调度。 |  
| GetTaskState（获取任务状态）                                         | GetTaskState（获取任务状态）          | TaskID（任务ID）     | 获取指定任务的状态。                                             |  
| TerminateTask（终止任务）                                            | TerminateTask（终止任务）             | 无                   | 如果当前任务状态为终止，则暂停当前任务。它不能在中断服务例程中调用。当前任务必须释放已获取的所有外部资源。 |  
| ChainTask（链接任务）                                                | ChainTask（链接任务）                 | TaskID（任务ID）     | 挂起当前任务，激活另一个处于暂停状态的任务，并将其放入待执行队列中。如果任务调度基于用户定义的调度策略，则在中断服务时无法执行此API。 |  
| 获取任务ID                                                           | （此列无对应状态类型/函数名，可省略） | 无（或根据上下文确定） | 获取当前正在运行的任务的ID。                                     |  
| 获取当前运行任务（可能是一个函数描述，或根据上下文可合并到上一行中） | （此列无对应状态类型/函数名，可省略） | 无（或根据上下文确定） | 执行获取当前正在运行的任务的操作（此条可能需要根据实际内容调整，或合并到上一行中并修改描述）。 |  
  
