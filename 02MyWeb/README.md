> [!NOTE]
>
> webserver服务器项目学习记录

✅[牛客Linux高并发服务器](https://www.nowcoder.com/courses/cover/live/504)：对于每部分主要的函数使用方法介绍，源于游双的书，项目实现后面省略了很多。

---

项目来源：[TinyWebServer](https://github.com/qinguoyi/TinyWebServer)

✅[环境配置]()：待补

​	⬜CMAKE

源码阅读

​	✅封装类

​	⬜HTTP报文解析

​	⬜定时器

​	⬜日志

​	⬜压力测试

⬜功能增加

<details> <summary>Linux shell常用命令</summary>  

```shell
vi 文件： 回车后就进入进入编辑模式，按 o 进行编辑
编辑结束，shift+：退出编辑模式，然后输入退出命令：
1.保存不退出：
:w 保存文件但不退出vi 编辑
:w! 强制保存，不退出vi 编辑
:w file 将修改另存到file中，不退出vi 编辑
2.保存并退出：
:wq 保存文件并退出vi 编辑
:wq! 强制保存文件并退出vi 编辑
3.不保存并退出：
q: 不保存文件并退出vi 编辑
:q! 不保存文件并强制退出vi 编辑
:e! 放弃所有修改，从上次保存文件开始在编辑

touch a.txt 创建一个txt文档
man 2/3   查看手册

ifconfig #查IP地址

# 查看查用的网络信息
netstat
	-a 所有的socket
	-p 显示正在使用IP地址，而不通过域名服务器
	-n 直接使用IP地址，而不通过域名服务器
```

```shell
int main(argc, char *argv[])

argc 是命令行总的参数个数
argv[] 是argc个参数，其中第0个参数是程序的全名，以后的参数命令行后面跟的用户输入的参数
```

</details>



