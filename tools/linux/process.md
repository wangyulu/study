# Linux进程常用命令

* **进程查看**
  * ps aux （unix格式查看）
    > a：所有前台进程 <br/>
      u：显示进程由哪个用户产生的 <br/>
      x：所有后台进程
    ```
    [root@localhost ~]# ps aux
    USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
    root         1  0.0  0.0   2904  1428 ?        Ss   May23   0:01 /sbin/init
    root         2  0.0  0.0      0     0 ?        S    May23   0:00 [kthreadd]
    root         3  0.0  0.0      0     0 ?        S    May23   0:02 [migration/0]

    USER：该进程由哪个用户产生的
    PID：进程的ID号
    %CPU：该进程占用CPU资源的百分比，占用越高，进程越耗费资源
    %MEM：该进程占用物理内存的百分比，占用越高，进程越耗费资源
    VSZ：该进程占用虚拟内存的大小，单位KB
    RSS：该进程占用实际物理内存的大小，单位KB
    TTY：该进程是在哪个终端中运行的。其中tty1-tty7代表本地控制台终端，tty1-tty6是本地的字符界面终端，tty7是图形终端。pts/0-256代表虚拟终端
    STAT：进程状态。常见的状态有：R（运行）、S（睡眠）、T（停止）、s（包含子进程）、+（位于后台）
    START：该进程的启动时间
    TIME：该进程占用CPU的运算时间（注意不是系统时间）
    COMMAND：产生此进程的命令名
    ```
  * ps -le （linux格式查看）
    > l：进程详细信息 <br/>
      e：所有进程

  * pstree [选项]
    > -p：显示进程的PID （后面加进程PID则显示指定进程的树）<br/>
      -u：显示进程的所属用户 <br/>

* **终止进程**
  * kill [选项]
    > 

