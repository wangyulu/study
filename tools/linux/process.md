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
    > 1（信号代码） SIGHUP（信号名称），该信号让进程立即关闭，然后重新读取配置文件后重启 <br/>
      2 SIGINT，程序终止信号，用于终止前台进程。相当于ctrl+c快捷键 <br/>
      9 SIGKILL，用来立即结束程序的运行，本信号不能被阻塞、处理和忽略。一般用于强制终止进程 <br/>
      15 SIGTERM，正常结束进程的信号，kill命令的默认信号。有时如果进程已经发生问题，这个信号是无法正常终止信号的，我们都会尝试SIGKILL信号，也就是信号9

  * killall [选项][信号] 进程名 （**按照进程名杀死进程**）
    > -i：交互式询问是否要杀死某个进程 <br/>
      -I：忽略进程名的大小写

  * pkill [选项][信号] 进程名 （**按照进程名杀死进程**）
    > -t：终端号，按照终端号踢出用户
    ```
    pkill -9 -t pts/30
    ```

* **进程相关其它命令**
  * lsof [选项] （**列出进程打开或使用的文件信息**）
    > -c 字符串：只列出以字符串开头的进程打开的文件 <br/>
      -u 用户名：只列表某个用户的进程打开的文件 <br/>
      -p pid：列出某个PID进程打开的文件 <br/>

  * 把进程放入后台
    * 在命令后加一个 & 符（命令放入后台运行）
      > tar -zcf ect.tar.gz /etc &
    * ctrl+z（命令暂停，然后放入后台）
      > top

  * 查看放入后台的进程
    > jobs -l <br/>
      -l：显示工作的PID <br/>

      <br/>
      **“+”：**代表最近一个放入后台的工作，也是工作恢复时默认恢复的工作 <br/>
      **“-”：**代表倒数第二个放入后台的工作

  * 将后台暂停的进程恢复到前台执行
    > fg %工作号 <br/>
      %工作号：%号可以省略（注意工作号与PID的区别）

  * 将后台暂停的进程恢复到后台执行
    > bg %工作号 <br/>

    **注：**将后台暂停的进程恢复到后台执行，是不能与前台有交互的，否则不能恢复到后台执行

