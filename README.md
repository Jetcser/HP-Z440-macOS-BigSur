# HP-Z440-macOS-Catalina

OpenCore版本0.7.6，编辑config.list推荐ProperTree，如果用OCC，务必使用对应版本。

硬件：
HP Z440 （X99）
处理器：E5-1650v3 （Haswell-E）
显卡：Nvdia Quadro K4200 (GK104）
无线网卡：Fenvi BCD94360CD
系统硬盘：Intel S3610 200GB （SATA）
数据硬盘：Toshiba P300 3TB (exFAT）
macOS版本：Catalina 10.5.7

ACPI：
1.Z440的BIOS版本更新到最新版的2.57；
2.SSDT-EC-Z440.aml 只是仿冒EC设备，Z440的ACPI表没有找到EC设备；
3.SSDT-HPET.aml 使用SSDTTime生成的，主要解决IRQ中断的问题，对比原始ACPI表之后发现，原理是把RTC设备IRQ8和TMR设备的IRQ0去除并作用到HPET设备上，不然启动过程中会Kernel Panic，要配合config.plist上的APCI->Patch使用，别忘了。
4.SSDT-PLUG-Z440.aml 解决CPU电源的睿频问题，同时要在config.plist里面Kernel->Emulate->Cpuid1Data中把仿冒ID填好，具体CPU的仿冒数据去查一下就知道了，比如E5-1650v3架构是Haswell-E，就去查这个架构对应的仿冒ID。
5.SSDT-RTC0-RANGE-Z440.aml RTC补丁，具体作用我忘了 -.-！
6.SSDT-UNC.aml 通用的UNC补丁，具体作用查dortania.github.io。
7.SSDT-MEM2-add.aml，SSDT-SLPB-add.aml，SSDT-SMBUS-MCHC-add.aml是自己加的，仿冒这几个设备用，好像用不用都能开机，有空可以自己研究下。

Kernel：
这部分就是常用的那些Kexts，比如Lilu，Whatevergreen，VirtualSMC及传感器，AppleALC，还有Intel板载网卡之类，这些都是通用的，不再赘述。

需要注意的是USB端口定制，Z440是X99平台。我已经定制好了，文件名是USBMap.kext，默认对应机型iMacPro1,1。如果你用机型MacPro6,1，请更换这个文件，对应的文件放在Kexts->off。
  如果想自己动手的话，最好最简单的方式是在Windows下用USBToolbox来操作，具体方法参见：
https://heipg.cn/tutorial/customize-usb-port-windows.html。

NVRAM：

boot-args参数 npci=0x2000 alcid=11 -v

npci=0x2000是X99平台必需的。

alcid是AppleALC驱动需要的，对于Z440的声卡，类型是ALC221，layout-id是11。

-v是开启字符模式，开机过程显示各种字符信息，用来排错，安装好了去掉，去掉之后需要Reset NVRAM才生效。

PlatformInfo：
  
机型采用的是iMacPro1,1，我已经把序列号啥的删除了，你需要用OCC重新生成相应的序列号。
如果买了免驱无线网卡，诸如Fenvi-BCM94360CD，来登录AppleID的话，还需要用网卡MAC来生成ROM。
详情见https://heipg.cn/tutorial/macserial-and-iservice-opencore.html

  另外需要注意的是，Kexts目录里面的USB端口定制文件USBMap.kext是对应机型的。
  如果你乐意的话，也可以用MacPro6,1，需要再强调一下的是，注意更换对应的USBMap.kext，两个版本的文件放在Kexts->off里面，用的时候改一下名就行了。


*更多知识查询dortania.github.io
