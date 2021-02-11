# 潮5000升级Big sur 正式EFI文件

需要注意的是，我发布的EFi文件就是我现在电脑上使用的EFi引导文件，所以没有考虑兼容性，如果不兼容的话需要自己对照我的电脑配置找一下差异做一个简单的修改，**完美99%**

------

电脑配置（网卡换成了**Intel@ac3168**无线网卡）：

其他配置看图

![联想小新潮5000-i7-7500u](https://gitee.com/masonsxu/cloudimg/raw/master//img/%E8%81%94%E6%83%B3%E5%B0%8F%E6%96%B0%E6%BD%AE5000-i7-7500u.jpg)

------

**更新**

> 2/11/2021

1. 删除 `VoodooPS2Controller.kext/Contents/PlugIns/VoodooInput.kext`
2. 删除 `VoodooPS2Controller.kext/Contents/PlugIns/VoodooPS2Mouse.kext`
3. 删除 `VoodooPS2Controller.kext/Contents/PlugIns/VoodooPS2Trackpad.kext`
4. 调整 `kext`  驱动加载顺序(调整顺序的样例来源：[常见驱动加载顺序]( https://github.com/daliansky/OC-little/tree/master/%E5%B8%B8%E8%A7%81%E9%A9%B1%E5%8A%A8%E5%8A%A0%E8%BD%BD%E9%A1%BA%E5%BA%8F))
5. 添加 `FCAP.aml` 并开启  `ACPI\Quirks\FadtEnableReset` 选项，能够开启长按开机键开启睡眠功能
6. 添加 `SSDT-TPD0.aml` ，并在 `ACPI\Patch` 添加补丁信息
7. 修改缓冲帧补丁，更换 `平台 id` 为 `0x591B0000`

> 1/30/2021

1. 完善 **USBPorts.kext**，解除端口限制（教程链接看[这里](https://blog.daliansky.net/Intel-FB-Patcher-USB-Custom-Video.html)）。
2. 使用 **CPUFriend.kext** 使CPU睿频，`注意看睿频前提`（教程看[这里](https://blog.xjn819.com/post/opencore-guide.html#4-0-OpenCore-进阶)）。
3. 添加了 **NoTouchID.kext** 驱动。

> 1/22/2021

1. 更新 OC 为 0.6.5。
2. USB驱动 **USBPorts.kext** 为定制驱动，如果出现不能正常使用，可以使用 **Hackintool** 自己生成定制驱动（USBPorts.text）。
3. 删除图形引导界面。
4. 更新各驱动版本为最新。
5. 解锁 **CFG Lock** （未解锁的请看 [这里](https://blog.csdn.net/one_a_xiaobai/article/details/109705321)）。

> 11/16/2020

1. 删除 ACPI 中一些不必要的补丁，成功解决`电池`和`触摸板`不能正常显示的问题。
2. 删除了Drivers中不需要的`*.efi`文件。
3. 删除了Tools中不需要的`*.efi`文件。

------

⚠️注意：

1. *触摸板驱动已经可以正常加载，手势也可用*，此引导**触摸板 ID** 为（ACPI\VEN_ELAN&DEV_0608），如果出现不能正常使用的情况请自行更换驱动。

2. *精简驱动文件数量，目前已经精简到了15个文件。*

3. *精简了ACPI文件夹中的文件，删除了一些对系统没有作用的 **.aml**文件。*

4. *通过添加 pci编码使得 VirtualSMC.kext 可以加载原生电源管理驱动，通过查看系统报告—>功能扩展—>**AppleLPC** 查看是否加载，如果没有加载请自己修改相关  **pci**，修改方法 https://www.bilibili.com/read/mobile/6353697 如果找不到的话也可以通过 **Hackintool的 PCI** 选项卡看。*

   <img src="https://gitee.com/masonsxu/cloudimg/raw/master//img/image-20201114195956032.png" alt="image-20201114195956032"  />

⚠️解决的问题：

- 有线网卡。
- 英特尔无限网卡。
- 蓝牙。
- 声卡。
- 触摸板（ELAN）手势可用，~~但是系统偏好设置里面没有检测到~~，并且系统可以检测到手势功能全部可用。
- 摄像头。
- 外接键盘、鼠标。
- 亮度可通过外接键盘设置快捷键调节。
- 睡眠再开机短时间内未出现问题。
- 可以加载原生电源管理驱动（AppleLPC.kext），~~节能4项可用，但是电池节能选项只有两项~~，电池选项全部可用，只不过系统报告中显示的（经测试不影响使用）。
  - Pack Lot Code：	0。
  - PCB Lot Code：	0。
  -  固件版本：	0
  -  硬件校正：	0
  -  电池校正：	0

⚠️未解决的问题：

- ~~电源图标不显示，电量显示为0~~
- ~~触摸板手势不能用~~
- ~~EFI文件未精简（我尝试着精简文件了，但是没成功，如果有成功的大佬记得分享😄）~~

（⚠️在这里提醒各位如果使用这个EFI文件，当完成引导后记得修改三码）

🎉🎉🎉参考文章：

xjn：[使用 OpenCore 引导黑苹果](https://blog.xjn819.com/post/opencore-guide.html)

黑果小兵：Hackintool(Intel FB Patcher) USB定制视频

