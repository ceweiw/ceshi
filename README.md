# 微实时操作系统特性概述  
  
以下是一个微实时操作系统的关键特性列表：  
  
- **内核大小**：  
  - 小于10千字节，确保了操作系统的轻量级和高效性。  
  
- **堆栈切换时间**：  
  - 小于8微秒，保证了任务切换的快速响应。  
  
- **中断响应时间**：  
  - 小于36微秒，确保了系统对外部事件的及时响应。  
  
- **符合标准**：  
  - 符合OSAEK OS、OAEK COM和OAEK OIL标准，提高了系统的兼容性和可靠性。  
  
- **调度机制**：  

*Features*:
1.Ultra-micro real-time operating system kernel:
1)Kernel size < 10k
2)Context switch time < 8us
3)Interrupt response time < 36us
2.Complies with OSEK OS, OSEK COM, OSEK OIL standards:
1)OSEK standard-compliant API
2)OSEK standard-compliant system development process
3)OSEK standard-compliant external communication mechanisms
3.Supports multiple scheduling mechanisms:
1)Preemptive scheduling
2)Non-preemptive scheduling
3)Hybrid scheduling
4.Supports static configuration
5.Supports various mainstream embedded processors
