## linux内核初探

### 一、操作系统和工具
- ubuntu操作系统20.04.3
- JDK8

### 二、系统调用实践

示范一段HelloWorld程序，其中有一行进行IO输出操作
```java
public class Hello {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
```

经过编译后，使用strace进行监控启动
```shell
strace -ff -o out java Hello
```
可以发现生成大量的输出文件，jdk较低版本主要看第一个输出文件，jdk中高版本看第二个输出文件，我们这里看第二个输出文件。
![strace追踪系统调用](../img/linux/strace-kernel.png)

我们可以在文件中找到write这个系统调用。实际上当程序调用此系统调用时会触发软中断，用户态切换内核态，由内核执行系统调用函数write

![系统调用write](../img/linux/system-call-write.png)

可以使用man学习系统调用函数
```
man write
```
![查看系统调用](../img/linux/man-write.png)

### 三、linux文件概念
建立本地客户端与百度域名的TCP连接并访问和打印
```shell
exec fd<> /dev/tcp/www.baidu.com/80
echo -e "GET / HTTP/1.0\n" 1>& fd
cat 0<& fd
```

![建立tcp连接](../img/2021-11-18-nio/linux-file-descripter.png)

查看当前进程的所有文件
```shell
cd /proc/$$/fd
```

可以发现同一进程内多个文件描述符，每个文件描述符都指向一个目录文件，socket也是文件
![文件描述符](../img/2021-11-18-nio/linux-socket.png)