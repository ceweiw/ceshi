简介：
SmartOSEK平台针对我国汽车电子领域的汽车电控系统的自主国产需求，重点研制面向汽车电子控制、符合国际OSEK标准的嵌入式实时操作系统，并从易用性、可靠性、高效性出发，配套提供完整的集成开发环境工具。SmartOSEK OS实现了符合OSEK规范OS标准BCC1、ECC1，符合OSEK规范COM标准CCCA、CCCB，以及支持OSEK规范OIL实现，支持多种国际主流嵌入式芯片，同时，实现了包含图形化建模编程设计、可视化系统配置、可视化OIL解析和配置、图形化OS运行情况跟踪、图形化任务调度分析的配套工具集。

部署：
该仓库是SmartOSEK 2.0标准状态试用版，该版本是HCS12平台的版本，在CodeWarrior版本CW12 V3.1上编译通过，运行正常。
用户可以使用CW12的模拟器运行该程序，也可以使用P&E Multilink把程序烧到目标板上运行，运行结果将通过串口输出。
该版本在使用上和正式版本区别如下：
1.支持扩展状态。
2.任务调度方式为混合式（MIX）。如果想实现全抢占，可以把所有任务定义为可抢占；如果想实现非抢占，可以把所有任务定义为不可抢占。
3.不支持OS_HOOK_GET_SERVICEID，OS_HOOK_PARAM_ACCESS。
4.不支持内部通信。
5.系统内核不支持静态裁减。

特征：
1.超微型强实时操作系统内核：
1)内核大小 < 10k
2)上下文切换时间 < 8us
3)中断响应时间 < 36us
2.遵循OSEK OS、 OSEK COM、 OSEK OIL标准
1)符合OSEK标准的API
2)符合OSEK标准的系统开发流程
3)符合OSEK标准的内部和外部通讯机制
3.支持多种调度机制：
1)可抢占调度
2)不可抢占调度
3)混合调度
4.支持静态配置
5.支持多种主流嵌入式处理器








API列表：

任务管理机制	StatusType ActivateTask (TaskType TaskID)：符合判断条件的情况下，激活一个处在suspend状态的任务，使其进入就绪队列，然后根据用户定义的调度策略执行任务调度。
	StatusType TerminateTask( void )：符合判断条件的情况下，将当前任务挂起。不能在中断处理函数调用。当前任务必须已经释放申请的外部资源,挂起后根据用户定义的调度策略执行任务调度。
	StatusType ChainTask (TaskType TaskID): 符合判断条件的情况下，挂起自己并且激活一个处在suspend状态的任务（TaskID），使其进入就绪队列, 根据用户定义的调度策略执行任务调度。该API不能在中断处理函数调用,当前任务必须已经释放申请的外部资源。

	StatusType GetTaskID( TaskRefType PTaskID )：得到当前运行任务的ID
	StatusType GetTaskState ( TaskType TaskID, TaskStateRefType state )：得到指定任务(TaskID)的状态
中断机制	void EnableAllInterrupts ( void )：打开所有中断DisableAllInterrupts
	void DisableAllInterrupts ( void )：屏蔽所有中断，不保留屏蔽期间触发的中断
	void SuspendAllInterrupts(void)：屏蔽所有中断，保留屏蔽期间触发的中断
	void ResumeAllInterrupts(void)：打开所有中断，对应SuspendAllInterrupts
	void SuspendOSInterrupts(void)：屏蔽二类中断，保留屏蔽期间触发的中断
	void ResumeOSInterrupts(void)：打开二类中断，对应SuspendOSlInterrupts
Alarm机制	StatusType GetAlarmBase ( AlarmType  AlarmID,AlarmBaseRefType Info )：查询counter状态,获得ID号为<AlarmID>的Alarm的counter的信息
	StatusType GetAlarm( AlarmType AlarmID, TickRefType	tick )：查询alarm状态，获得ID号为<AlarmID>的Alarm现在时刻到触发时间的相对ticks值，并返回
	StatusType	SetRelAlarm( AlarmType AlarmID, TickType increment, TickType cycle )：该函数被调用以后，将占用id号为<AlarmID>的Alarm，然后在经过<increment>个时钟ticks之后，将触发相应的任务或者相应的事件将被置位,若Cycle != 0则再每经过Cycle个TICKS后触发ALARM
	StatusType	SetAbsAlarm( AlarmType AlarmID, TickType start, TickType cycle )：该模块被调用以后，将占用id号为<AlarmID>的Alarm，然后在当系统时钟数为<start>时，将触发相应的任务或者相应的事件将被置位,若Cycle != 0则再每经过Cycle个TICKS后触发ALARM.
	StatusType	CancelAlarm( AlarmType AlarmID )：取消ID号为<AlarmID>的Alarm的使用
事件机制	StatusType SetEvent( TaskType TaskID, EventMaskType Mask)：根据Mask来设置TaskID所表示任务的事件，一旦改任务所等待的事件中有一个被置位，该任务就进入就绪状态,然后根据用户定义的调度策略执行调度。该API只对非挂起状态的扩展任务有效。
	StatusType ClearEvent( EventMaskType Mask)：根据Mask来清除当前任务的事件。只对扩展任务有效，不能在中断级别调用
	StatusType GetEvent( TaskType TaskID, EventMaskRefType Event)：返回TaskID所表示任务的事件状态。只对非挂起状态的扩展任务有效。
	StatusType WaitEvent( EventMaskType Mask)：使当前任务进入等待状态直到有Mask表示的事件发生。如果等待的事件已经被置位，则任务继续进行，不发生调度。只对扩展任务有效，不能在中断级别调用。该任务应该已经释放了申请的外部资源。
资源管理机制	StatusType GetResource ( ResourceType resId )：当前任务得到resId的外部资源或调度器资源, 设置任务优先级为资源的优先级。
	StatusType ReleaseResource ( ResourceType resId )：释放当前任务拥有的外部资源或调度器资源, 恢复任务优先级，然后根据用户定义的调度策略执行任务调度。
内部通信	StatusType StartCOM (COMApplicationModeType mode)：启动COM，同时完成消息对象初始化。
StatusType StopCOM  ( COMShutdownModeType mode )：停止COM。
COMApplicationModeType GetCOMApplicationMode (void)：当前COM的工作模式
	StatusType InitMessage(SymbolicName message, ApplicationDataRef dataref)：初始化消息指针。
	FlagValue ReadFlag_<Flag>()：读取Flag标志位。具体Flag值参加该宏的列表；每个Flag均对应一个ReadFlag_<Flag>宏。
	void ResetFlag_<Flag>()：设置Flag标志位。
	StatusType SendMessage(SymbolicName message, ApplicationDataRef data)：把dataref里的数据发送到发送消息对象message里。
	StatusType ReceiveMessage(SymbolicName message, ApplicationDataRef data)：把接收消息对象message里的数据接收到data里，并更新参数message相关联的所有flag。
	StatusType SendZeroMessage(SymbolicName message)：消息数据为零长度，没有发送动作；但需根据消息对象配置信息启动消息机制。
	StatusType GetMessageStatus(SymbolicName message)：消息数据为零长度，没有发送动作；但需根据消息对象配置信息启动消息机制。
	#define COMErrorGetServiceId(void) ServiceId：获得出错API的ServiceId。
	StatusType StartCOMExtension(void)：用户配置的COM初始化操作。根据宏COM_START_EXTENTSION是否配置来确定是否在StartCOM中调用。
	void COMErrorHook(StatusType Error)：用户配置的COM出错后的hook函数。
	void COMErrorHook(StatusType Error)：用户配置的COM出错后的hook函数。Name1为出错API的名称；Name2为出错API的错误参数的名称。系统已经为所有API及其参数的搭配定义好这个宏，用户可以直接调用。

