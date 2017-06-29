## Native Heap使用

1. 检查两个so文件

	```
	/system/lib/libc_malloc_debug_leak.so 
	/system/lib/libc_malloc_debug_qemu.so   
	```

2. 告知系统使用新的库分配内存

	```
	adb shell
	su
	setprop libc.debug.malloc 1  
	```	

3. 重启框架

	 如果命令成功，设备将在 1、 2 秒后重启， 注意并不是完全重启。
	 
	```
	stop  
	start 
	```

4. 检查是否正常

	```
	getprop
	```

	会得到包含以下信息的内容 "[libc.debug.malloc]: [1]"
	
	
5. 配置ddms.cfg

	找到用户目录下 **.android**文件夹，打开其中的 **ddms.cfg**,并向其中添加
	
	```
	native=true
	```
	
6. 打开DDMS

	点击snapshot current... 按钮就可以了
	

**注意：**  
找到自己的库函数***.so**后面的 **Method** 列中的地址。使用 NDK 中的 addr2line 工具

**Method** 中的地址一般要将高 3 位置 0 ， a4745183 变为 00045183
