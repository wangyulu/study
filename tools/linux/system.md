# Linux系统常用命令

* **健康状况查看**
  * top [选项]
    > -d：指定top命令每隔几秒更新，默认3秒 <br/>
      在top命令的交互模式当中可以执行的命令：<br/>
      ？或h：显示交互模式的帮助 <br/>
      P：以CPU使用率排序，默认就是此项 <br/>
      M：以内存的使用率排序 <br/>
      N：以PID排序 <br/>
      q：退出top <br/>
      ```
      [root@localhost ~]# top
      top - 23:13:52 up 1 day, 13:50,  1 user,  load average: 0.04, 0.02, 0.00
      Tasks: 162 total,   1 running, 161 sleeping,   0 stopped,   0 zombie
      Cpu(s):  0.0%us,  0.0%sy,  0.0%ni, 99.9%id,  0.0%wa,  0.0%hi,  0.0%si,  0.0%st
      Mem:   5026784k total,   452572k used,  4574212k free,   109644k buffers
      Swap:  2555900k total,        0k used,  2555900k free,   212532k cached

      top - 23:13:52 up 1 day, 13:50：系统当前时间：23:13:52 系统自开机以来运行了1天13小时50分钟
        1 user：表示登录了1个用户
        load average: 0.04, 0.02, 0.00：系统在1分钟、5分钟、15分钟之前的平均负载（如果CPU是一核，负载为1.04 1.02 1.00时，则表示负载较高 重要）
      Tasks（进程）：
        162 total：表示总共有162个进程
        1 running：1个进程正在运行
        161 sleeping：161个进程睡眠
        0 stopped：0个进程正在停止
        0 zombie：0个僵死进程（表示正在终止，但是终止没有完成）
      Cpu(s)：
        0.0%us：用户占用的CPU百分比
        0.0%sy：系统占用的CPU百分比
        0.0%ni：改变过优先级的用户进程占用的CPU百分比
        99.9%id：空闲CPU的CPU百分比（重要）
        0.0%wa：等待输入/输出进程的占用CPU百分比
        0.0%hi：硬中断请求服务占用的CPU百分比
        0.0%si：软中断请求服务占用的CPU百分比
        0.0%st：st（steal time）虚拟时间百分比，就是当有虚拟机时，虚拟CPU等待实际CPU的时间百分比

      Mem（内存）：
        5026784k total：物理内存总大小
        452572k used：物理内存已使用大小
        4574212k free：物理内存空闲大小（重要）
        109644k buffers：缓冲内存大小

      Swap（交换分区）：
        2555900k total：交换分区（虚拟内存）的总大小
        0k used：交换分区已使用大小
        2555900k free：交换分区空闲大小
        212532k cached：作为缓存的交换分区大小
      ```