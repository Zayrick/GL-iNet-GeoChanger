# GL iNet 路由器更改区域指南

本教程旨在指导用户如何在不同型号的 GL iNet 路由器上更改区域设置。请注意，此操作涉及直接写入闪存，存在一定风险。操作前请确保充分理解每一步骤，并小心谨慎地执行。

## 风险警告
- 直接写入闪存可能导致设备无法启动。
- 请在操作前仔细阅读教程，确保操作步骤无误。
- 操作过程中，请谨慎执行每一步。

## 准备工作
在开始之前，请确保您已经备份了路由器的重要数据。更改区域设置前，建议查看当前的分区信息以确认写入的位置。您可以在路由器已安装的 OpenWRT 系统中使用以下命令查看分区信息：

```bash
lsblk
# 或
fdisk -l
```

## 更改区域操作步骤

为了避免误操作导致设备损坏，请务必按照**“检查 -> 更改 -> 验证 -> 重启”**的顺序执行。

### MT3600BE 路由器

1. **检查当前区域代码**：
   确认输出中包含当前的区域代码。如果检查时发现区域代码不为CN，请勿继续，并提交issue。
   ```bash
   dd if=/dev/mtdblock3 bs=1 count=2 skip=16520 2>/dev/null | hexdump -C
   ```

2. **更改为 US 区域**：
   ```bash
   echo -n "US" | dd of=/dev/mtdblock3 bs=1 seek=16520 conv=notrunc
   sync
   ```

3. **验证更改结果**：
   确认输出已显示为 `US`。
   ```bash
   dd if=/dev/mtdblock3 bs=1 count=2 skip=16520 2>/dev/null | hexdump -C
   ```

4. **重启设备**：
   ```bash
   reboot
   ```

### MT3000 路由器

1. **检查当前区域代码**：
   确认输出中包含当前的区域代码。如果检查时发现区域代码不为CN，请勿继续，并提交issue。
   ```bash
   dd if=/dev/mtdblock3 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

2. **更改为 US 区域**：
   ```bash
   echo -n "US" | dd of=/dev/mtdblock3 bs=1 seek=136 conv=notrunc
   sync
   ```

3. **验证更改结果**：
   确认输出已显示为 `US`。
   ```bash
   dd if=/dev/mtdblock3 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

4. **重启设备**：
   ```bash
   reboot
   ```

### MT2500 路由器

1. **解除写保护并检查区域**：
   如果检查时发现区域代码不为CN，请勿继续，并提交issue。
   ```bash
   echo 0 > /sys/block/mmcblk0boot1/force_ro
   dd if=/dev/mmcblk0boot1 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

2. **更改为 US 区域**：
   ```bash
   echo -n "US" | dd of=/dev/mmcblk0boot1 bs=1 seek=136 conv=notrunc
   sync
   ```

3. **验证更改结果**：
   确认输出已显示为 `US`。
   ```bash
   dd if=/dev/mmcblk0boot1 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

4. **重启设备**：
   ```bash
   reboot
   ```

### AX1800/AXT1800 路由器

1. **检查当前区域代码**：如果检查时发现区域代码不为CN，请勿继续，并提交issue。
   确认输出中包含当前的区域代码。
   ```bash
   dd if=/dev/mtdblock8 bs=1 count=2 skip=152 2>/dev/null | hexdump -C
   ```

2. **更改为 US 区域**：
   ```bash
   echo -n "US" | dd of=/dev/mtdblock8 bs=1 seek=152 conv=notrunc
   sync
   ```

3. **验证更改结果**：
   确认输出已显示为 `US`。
   ```bash
   dd if=/dev/mtdblock8 bs=1 count=2 skip=152 2>/dev/null | hexdump -C
   ```

4. **重启设备**：
   ```bash
   reboot
   ```

### MT6000 路由器

1. **检查当前区域代码**：
   确认输出中包含当前的区域代码。如果检查时发现区域代码不为CN，请勿继续，并提交issue。
   ```bash
   dd if=/dev/mmcblk0p2 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

2. **更改为 US 区域**：
   ```bash
   echo -n "US" | dd of=/dev/mmcblk0p2 bs=1 seek=136 conv=notrunc
   sync
   ```

3. **验证更改结果**：
   确认输出已显示为 `US`。
   ```bash
   dd if=/dev/mmcblk0p2 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

4. **重启设备**：
   ```bash
   reboot
   ```

### BE3600 路由器

1. **检查当前区域代码**：
   确认输出中包含当前的区域代码。如果检查时发现区域代码不为CN，请勿继续，并提交issue。
   ```bash
   dd if=/dev/mtdblock11 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

2. **更改为 US 区域**：
   ```bash
   echo -n "US" | dd of=/dev/mtdblock11 bs=1 seek=136 conv=notrunc
   sync
   ```

3. **验证更改结果**：
   确认输出已显示为 `US`。
   ```bash
   dd if=/dev/mtdblock11 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

4. **重启设备**：
   ```bash
   reboot
   ```

### GL-BE6500 路由器

1. **检查当前区域代码**：
   确认输出中包含当前的区域代码。如果检查时发现区域代码不为CN，请勿继续，并提交issue。
   ```bash
   dd if=/dev/mtdblock11 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

2. **更改为 US 区域**：
   ```bash
   echo -n "US" | dd of=/dev/mtdblock11 bs=1 seek=136 conv=notrunc
   sync
   ```

3. **验证更改结果**：
   确认输出已显示为 `US`。
   ```bash
   dd if=/dev/mtdblock11 bs=1 count=2 skip=136 2>/dev/null | hexdump -C
   ```

4. **重启设备**：
   ```bash
   reboot
   ```

## 重置固件
成功更改区域后，建议重置固件以确保所有设置正确应用。重置操作可以通过路由器的管理界面执行。

## 语言切换
若要查看某些特定区域的特定功能，请将系统语言从简体中文切换到繁体中文。可通过替换 `/www/i18n` 目录下的相应文件实现。

- 将文件名后缀为 `zh-cn` 的文件替换为 `zh-tw` 文件。

通过以上步骤，您可以在 GL iNet 路由器上成功更改区域设置。再次提醒，请在操作过程中保持高度警觉，以避免不必要的设备故障。

## 贡献者

<a href="https://github.com/Zayrick/GL-iNet-GeoChanger/graphs/contributors">
  <img src="https://contrib.rocks/image?repo=Zayrick/GL-iNet-GeoChanger" />
</a>
