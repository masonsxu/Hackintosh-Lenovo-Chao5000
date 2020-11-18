# 潮5000升级Big sur 正式EFI文件

该文件是由大佬（潮7000-13-i5-8250u QQ: 506184746）提供的潮7000-OC引导文件修改完成的，==**完美99%**==

------

**更新**

> 11/16/2020

1. 删除 ACPI 中一些不必要的补丁，成功解决`电池`和`触摸板`不能正常显示的问题
2. 删除了Drivers中不需要的`*.efi`文件
3. 删除了Tools中不需要的`*.efi`文件

------

==更正==：

1. *触摸板驱动已经可以正常加载，手势也可用*

2. *精简驱动文件数量，目前已经精简到了15个文件*

3. *精简了ACPI文件夹中的文件，删除了一些对系统没有影响的 ==.aml== 文件*

4. *通过添加 ==pci编码== 使得原生电源管理驱动可以加载，通过查看系统报告—>功能扩展—>AppleLPC 查看是否加载，如果没有加载请自己修改相关  ==pci== ，修改方法 https://www.bilibili.com/read/mobile/6353697 如果找不到的话也可以通过 ==Hackintool的 PCI 选项卡==查看*

   <img src="https://gitee.com/masonsxu/cloudimg/raw/master//img/image-20201114195956032.png" alt="image-20201114195956032"  />

⚠️解决的问题：

- 有线网卡
- 英特尔无限网卡
- 蓝牙
- 声卡
- 触摸板（ELAN）手势可用，~~但是系统偏好设置里面没有检测到~~，并且系统可以检测到手势功能全部可用
- 摄像头
- 外接键盘、鼠标
- 亮度可通过外接键盘设置快捷键调节
- 睡眠再开机短时间内未出现问题
- 可以加载原生电源管理驱动（AppleLPC.kext），~~节能4项可用，但是电池节能选项只有两项~~，电池选项全部可用，只不过系统报告中显示的（经测试不影响使用）
  - Pack Lot Code：	0
  - PCB Lot Code：	0
  -  固件版本：	0
  -  硬件校正：	0
  -  电池校正：	0

⚠️未解决的问题：

- ~~电源图标不显示，电量显示为0~~
- ~~触摸板手势不能用~~
- ~~EFI文件未精简（我尝试着精简文件了，但是没成功，如果有成功的大佬记得分享😄）~~

在这里感谢群内各位大佬提供的文件🙏。

（⚠️在这里提醒各位如果使用这个EFI文件，当完成引导后记得修改三码）

